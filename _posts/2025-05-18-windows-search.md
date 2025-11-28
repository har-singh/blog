---
layout: post
title: Disable Bing Search in Windows 10 Start Menu
date: 2025-05-18 13:40
author: har-singh
comments: true
categories: [blog]
---

If you're tired of web results cluttering your Start Menu search, here's how to **completely disable Bing integration** on Windows 10.

## 🛠️ Method: Group Policy (Worked for me)

### 1. Open Group Policy Editor

Run `gpedit.msc` (Win + R)

### 2. Navigate to:

```
Computer Configuration > Administrative Templates > Windows Components > Search
````

### 3. Enable the Following Policies:

- ✅ **Do not allow web search**
- ✅ **Don't search the web or display web results in Search**
- ✅ **Don't allow Cortana**

### 4. Apply Changes

- Run `gpupdate /force` in Command Prompt  
- Or simply **reboot**

## ⚠️ Note on Registry Tweaks

The following **did not work reliably**:
- `BingSearchEnabled = 0`
- `CortanaConsent = 0`
- `DisableSearchBoxSuggestions = 1`

Use **Group Policy** for consistent results.

## 🧼 Optional: Restart Explorer Manually

```cmd
taskkill /f /im explorer.exe && start explorer.exe
````

## ✅ Result

Start Menu search now works **offline only** — no Bing, no web results.
