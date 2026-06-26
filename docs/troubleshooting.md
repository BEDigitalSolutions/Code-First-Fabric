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

## Check Current Azure Account

```powershell
az account show
```

## Verify Download Hash

```powershell
Get-FileHash .\cff.exe -Algorithm SHA256
```

Compare output with release `checksums.txt`.
