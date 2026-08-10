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

## Storage Location or Migration

Code First Fabric stores pull history, push staging, and monitor cache under a shared storage root. If the default temp location is not suitable, set a secure persistent root:

```powershell
cff config hist-path C:\CFF
```

For a temporary pull-history override:

```powershell
$env:CFF_HIST_PATH = "C:\CFF\pull"
```

Show the effective path:

```powershell
cff config hist-path
```

`cff config hist-path` cannot change or reset the root while `CFF_HIST_PATH` is set. Unset it first:

```powershell
Remove-Item Env:CFF_HIST_PATH
```

If migration reports a conflict, the target contains a different file with the same relative path. Use an empty target or resolve the conflicting file before retrying. If it reports that old-root cleanup failed, the new root is already active; remove the reported old directory manually after checking the copied files.

## Local Monitor Does Not Start

Run without a fixed port to let Code First Fabric choose an available local port:

```powershell
cff view --no-open
```

If a fixed port is required, choose one not already in use:

```powershell
cff view --port 8080
```

Source-mode development requires Bun and the monitor source directory. Set `CFF_VIEW_DIR` to that directory when Code First Fabric cannot find it.

## Telemetry Settings

Check whether telemetry is available and effective in the installed build:

```powershell
cff telemetry status
```

Disable it for future commands:

```powershell
cff telemetry disable
```

`CFF_TELEMETRY_DISABLED=1` and `DO_NOT_TRACK=1` suppress telemetry in the current environment. For privacy information, see the [telemetry privacy notice](Aviso-privacidad-telemetria.md).

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
