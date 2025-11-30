---
layout: post
title: Azure Firewall Kusto Query - AZFW vs AzureFirewall Categories
date: 2025-11-29 11:45
author: har-singh
comments: true
categories: [azure]
---

Quick reference for querying Azure Firewall logs in Log Analytics using Kusto (KQL).

## AZFW vs AzureFirewall Categories

Azure Firewall logs come in two category formats:

- **AzureFirewall*** (legacy) — e.g. `AzureFirewallApplicationRule`, `AzureFirewallNetworkRule`
- **AZFW*** (resource-specific) — e.g. `AZFWApplicationRule`, `AZFWNetworkRule`

Microsoft recommends using the **AZFW** (resource-specific) tables. They're structured better and provide parsed fields out of the box — no need to manually extract data from a single `msg_s` column.

From Microsoft's documentation on resource-specific mode:

> This method is recommended since it:
> - might reduce overall logging costs by up to 80%
> - makes it much easier to work with the data in log queries
> - makes it easier to discover schemas and their structure
> - improves performance across both ingestion latency and query times
> - allows you to grant Azure RBAC rights on a specific table
>
> — [Monitor Azure Firewall](https://learn.microsoft.com/en-us/azure/firewall/monitor-firewall#resource-specific-mode)

## Query: Recent Firewall Traffic

This query returns application and network rule hits from the last 5 minutes, excluding internal traffic and DNS:

```kql
AzureDiagnostics
| where TimeGenerated > ago(5m)
| where Category in ("AZFWApplicationRule", "AZFWNetworkRule")
| where not(ipv4_is_in_range(SourceIP, "10.248.8.0/24")) and SourceIP != "10.248.30.21"
| where DestinationPort_d != 53
| project TimeGenerated, Category, SourceIP, DestinationIp_s, Fqdn_s, DestinationPort_d, Action_s, Rule_s
| order by TimeGenerated desc
```

### What the Query Does

| Filter | Purpose |
|--------|---------|
| `TimeGenerated > ago(5m)` | Last 5 minutes of logs |
| `Category in (...)` | Application and network rules only |
| `not(ipv4_is_in_range(...))` | Exclude internal subnet |
| `DestinationPort_d != 53` | Exclude DNS traffic |
| `project` | Return only relevant columns |

### Key Columns in AZFW Tables

| Column | Description |
|--------|-------------|
| `SourceIP` | Source IP address |
| `DestinationIp_s` | Destination IP |
| `Fqdn_s` | Fully qualified domain name (if applicable) |
| `DestinationPort_d` | Destination port |
| `Action_s` | Allow or Deny |
| `Rule_s` | Rule that matched |

## Why AZFW is Better

With the legacy `AzureFirewall*` categories, you'd need to parse the `msg_s` field manually:

```kql
| parse msg_s with Protocol " request from " SourceIP ":" SourcePort ...
```

With `AZFW*`, the fields are already split — just `project` and go.

## References

- [Azure Firewall log and metrics](https://learn.microsoft.com/en-us/azure/firewall/logs-and-metrics)
- [Resource-specific vs Azure Diagnostics mode](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/resource-logs#resource-specific)
