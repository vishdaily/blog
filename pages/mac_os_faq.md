---
layout: page
title: Mac Os FAQ
categories: [mac]
tags: [macos, mac]
type: page
---

# Commands

### launchctl
lists all running agents and daemons

```bash
launchctl list

#  prints out the root daemons, and only the root deamons.
sudo launchctl list

# one liner to get all the active daemons and their plist paths
grep -B 1 -A 1 "active count = 1$" <<< "$(launchctl dumpstate)"
```

# Paths

### Notification Agents
~/Library/Application Support/

### Loaded or Unloaded launch agents like to hide
|Path|Desc|
|----|----|
|~/Library/LaunchAgents|Per-user agents provided by the user|
|/Library/LaunchAgents|Per-user agents provided by the administrator.|
|/Library/LaunchDaemons|System wide daemons provided by the administrator.|
|/System/Library/LaunchAgents|OS X Per-user agents.|
|/System/Library/LaunchDaemons|OS X System wide daemons.|


