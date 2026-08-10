# Configuration

## Azure CLI Login

CFF uses Azure CLI credentials by default.

Default login:

```powershell
az login
```

Tenant has no Azure subscriptions:

```powershell
az login --allow-no-subscriptions
```

## Device Code Login

Use device code when browser login is blocked, remote shell used, or sign-in window cannot open.

```powershell
az login --use-device-code
```

Azure CLI prints code and URL. Open URL in browser, enter code, finish login, then run `cff login`.

## Tenant-Specific Login

Use tenant ID when account belongs to multiple tenants or CFF resolves wrong tenant.

```powershell
az login --tenant <tenant-id>
```

Device code + tenant:

```powershell
az login --use-device-code --tenant <tenant-id>
```

No-subscription tenant:

```powershell
az login --tenant <tenant-id> --allow-no-subscriptions
```

## Service Principal

Set environment variables when using service principal auth:

```powershell
$env:AZURE_CLIENT_ID = "<client-id>"
$env:AZURE_TENANT_ID = "<tenant-id>"
$env:AZURE_CLIENT_SECRET = "<client-secret>"
cff login
```

## Verify Login

```powershell
az account show
```

`cff login` prints credential type, token expiry, and token preview.

## CFF Storage

Code First Fabric uses a shared storage root for raw pull definitions, push staging, and the local monitor cache. These files can contain complete staged source copies, secrets, or sensitive configuration, so use a secure location.

Show the effective storage root and derived paths:

```powershell
cff config hist-path
```

Set a persistent storage root:

```powershell
cff config hist-path C:\CFF
```

Reset to the default storage root:

```powershell
cff config hist-path --reset
```

For `C:\CFF`, Code First Fabric stores data in `C:\CFF\pull`, `C:\CFF\push`, and `C:\CFF\view\cache`. The default storage root is under the operating system temp directory, for example `%TEMP%\cff` on Windows. Persistent config is stored in `%USERPROFILE%\.fabric-local-cli\config.json`.

When changing the root, Code First Fabric preflights the existing data, copies it, verifies the copies, then removes the old files. If a destination contains different files with the same relative path, the move stops without changing the configured root. If old-root cleanup fails after verification, the new root remains active and Code First Fabric reports the old location for manual cleanup.

For a one-session pull-history override, set `CFF_HIST_PATH`:

```powershell
$env:CFF_HIST_PATH = "C:\CFF\pull"
```

When `CFF_HIST_PATH` is set, it takes precedence for pull history. Unset it before running `cff config hist-path <rootPath>` or `cff config hist-path --reset`:

```powershell
Remove-Item Env:CFF_HIST_PATH
```

`CFF_VIEW_CACHE_DIR` overrides only the derived monitor-cache path. It is not moved when the storage root changes.
