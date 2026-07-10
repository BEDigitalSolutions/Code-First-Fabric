# Troubleshooting

## `cff` Not Found

Cause: folder containing `cff.exe` not in PATH or terminal not restarted.

Fix:

```powershell
$env:Path -split ";"
cff --help
```

Add folder to user PATH, then open new terminal.

## Azure Login Required

Run:

```powershell
az login
```

If tenant has no subscriptions:

```powershell
az login --allow-no-subscriptions
```

Then verify CFF can resolve a token:

```powershell
cff login
```

## Browser Login Fails

Use device code:

```powershell
az login --use-device-code
```

## Wrong Tenant

Force tenant:

```powershell
az login --tenant <tenant-id>
```

Device code + tenant:

```powershell
az login --use-device-code --tenant <tenant-id>
```

## Build Expired

Message says build expired. The installed executable was built with an expiration date. Download the latest release and replace `cff.exe`.

## Pull History Location

`cff pull` writes raw Fabric definitions to pull history. If the default temp location is not suitable, set a secure persistent path:

```powershell
cff config hist-path C:\CFF\history
```

For a temporary override:

```powershell
$env:CFF_HIST_PATH = "C:\CFF\history"
```

Show the effective path:

```powershell
cff config hist-path
```

## Protected Items Skipped During Pull

If a pull reports `ItemHasProtectedLabel`, the item has a protected sensitivity label. CFF skips that item and continues pulling the rest of the workspace.

Fix: remove or change the label if your governance policy allows it, then pull again. Otherwise, keep the item out of the local workspace copy.

## Usage Metrics Artifacts Skipped

Full or folder pulls skip Fabric usage metrics `Report` and `SemanticModel` artifacts by default. These are service-generated artifacts and may not export cleanly.

If you need one, run the explicit `cff pull` command printed in the warning to pull that artifact directly.

## SQL Notebook Rejected

`cff sql run file` accepts `.sql` files and SQL `.ipynb` notebooks only. If CFF says a notebook is not a SQL notebook, run a `.sql` file or use a notebook whose language metadata is SQL.

## Check Current Azure Account

```powershell
az account show
```

## Verify Download Hash

```powershell
Get-FileHash .\cff.exe -Algorithm SHA256
```

Compare output with release `checksums.txt`.
