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

## Pull History Path

`cff pull` stores raw Fabric definitions in pull history before writing the transformed local workspace tree. Raw definitions may contain secrets or sensitive configuration, so store pull history in a secure location.

Show the effective history path:

```powershell
cff config hist-path
```

Set a persistent history path:

```powershell
cff config hist-path C:\CFF\history
```

Reset to the default path:

```powershell
cff config hist-path --reset
```

The default path is under the operating system temp directory, for example `%TEMP%\cff\pull` on Windows. Persistent config is stored in `%USERPROFILE%\.fabric-local-cli\config.json`.

For a one-session override, set `CFF_HIST_PATH`:

```powershell
$env:CFF_HIST_PATH = "C:\CFF\history"
```

When `CFF_HIST_PATH` is set, it takes precedence over the configured path.
