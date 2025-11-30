---
layout: post
title: SNMP v3 on F5 BIG-IP
date: 2020-09-17 16:01
author: har-singh
comments: true
categories: [f5]
---

A post to document and share the commands required to configure the SNMP agent on an F5 device.

## Configuring SNMP via GUI

Via the GUI, the configuration is straightforward:

1. Allow NMS IP in the list at **System > SNMP > Agent > Configuration**  
   - I had to struggle here as the `snmpwalk` test was working from the BIG-IP box when pointing to localhost (`127.0.0.1`), but the `snmpwalk` against the management IP didn't work.  
   - By default (as F5 is a default deny device), SNMP requests are blocked.

2. Add a user by navigating to **System > SNMP > Agent > Access (v3)**  
   - More information about authentication type, privacy protocol, and security level can be retrieved from the F5 knowledge base article:  
     [K13625](https://support.f5.com/csp/article/K13625)

> [!NOTE]  
> The **OID** field is mandatory, but it wasn't clear what to enter. The KB article suggests that specifying `.1` will retrieve all MIBs.

## Configuring SNMP via CLI

I created a user via the GUI and then ran the following command to get the syntax:

```sh
show running-config sys snmp users
sys snmp {
    users {
        idemo_1 {
            auth-password-encrypted "XICfN\?MFr6CM=jHBg^p]VM;IUPkcY7jY@q\?=BRd/^HjSX8I"
            auth-protocol sha
            oid-subset .1
            privacy-password-encrypted 9b<L`=8:qgB_3\CIJo8OjR)iLPPwH30_TbSAWLfoeQi\?i6W
            privacy-protocol aes
            security-level auth-privacy
            username demo
        }
    }
}
```

From this, I created a command that can be issued directly to the CLI to create the user:

```sh
modify sys snmp allowed-addresses add { 10.0.0.0/255.0.0.0 }

modify sys snmp users add { snmpuser-entry {  
    auth-password "MakeUpSomePassword"  
    auth-protocol sha  
    oid-subset .1  
    privacy-password "MakeUpSomePassword"  
    privacy-protocol aes  
    security-level auth-privacy  
    username snmpuser  
} }
```

## Testing SNMP Configuration
You can test the SNMP configuration using the following command:

```sh
snmpget -v3 -u snmpuser -a SHA -A "MakeUpSomePassword" -x AES -X "MakeUpSomePassword" -l authPriv 192.168.1.245 iso.3.6.1.2.1.1.5.0
```

### Expected Output:

```sh
iso.3.6.1.2.1.1.5.0 = STRING: "bigip1.f5lab.com"
```

## Additional Resources
The knowledge base article [K12601](https://support.f5.com/csp/article/K12601) has been reported as archived, but it was very useful in understanding these commands.
