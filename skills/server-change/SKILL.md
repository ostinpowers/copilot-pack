---
name: server-change
description: "Plans and makes one change on a Linux or Windows server: confirm the host, read its state, back up, change, verify, keep the rollback ready. Use when changing a server's config, service or package."
---

# A change on a server

## Steps

1. Confirm the target is the one meant: its hostname and OS
   (`hostnamectl`; `Get-ComputerInfo -Property CsName, OsName, OsVersion`).
2. Read its current state first: the file to change, the service
   (`systemctl status <service>`; `Get-Service <service>`), recent log lines
   (`journalctl -u <service> -n 50`; `Get-WinEvent -LogName System -MaxEvents 50`).
3. Write the rollback before the change: the exact commands that undo it.
4. Back up what changes, with the date:
   `cp -p <file> <file>.bak-$(date +%F)`;
   `Copy-Item <file> "<file>.bak-$(Get-Date -Format yyyy-MM-dd)"`.
5. Show the plan and wait for the user's yes. Where the tool has a preview,
   run it first: `-WhatIf`, `--dry-run`, `--check`.
6. Change one thing, then verify: the service runs, the port answers, the log
   is clean. If not, roll back and report.

## Done when

- The change is in, verified, and the backup and rollback are written down.
