---
name: cloud-read-first
description: "Looks into AWS or Azure with read-only CLI calls, confirming account, subscription and region first, and keeps output short. Use before any cloud change, or when asked what exists or why."
---

# Cloud, read first

## Steps

1. Who and where, said before anything else:
   - AWS: `aws sts get-caller-identity` and `aws configure get region`.
   - Azure: `az account show --query "{name:name, id:id}" -o table`.
2. Read only: describe, list, show, get. Narrow every call to a resource
   group, a tag or a name; select fields with `--query`; print with
   `-o table` or `--output text`; cap lists with `--max-items`.
3. Filter a large result before reading it; never bring a whole JSON listing
   into the chat.
4. A change (create, update, delete, start, stop, scale, tag) becomes a plan
   for the user, with its rollback and its cost; it runs only after their yes.
5. Keys, connection strings and tokens stay unprinted: refer to the vault
   entry instead (Key Vault, Secrets Manager).

## Done when

- The answer names the account or subscription and region it came from, and
  quotes the commands that gave it.
