# Configuration

## Azure CLI Login

CFF uses Azure CLI credentials by default.

Default login:

```powershell
az login
cff login
```

Tenant has no Azure subscriptions:

```powershell
az login --allow-no-subscriptions
cff login
```

## Device Code Login

Use device code when browser login is blocked, remote shell used, or sign-in window cannot open.

```powershell
az login --use-device-code
cff login
```

Azure CLI prints code and URL. Open URL in browser, enter code, finish login, then run `cff login`.

## Tenant-Specific Login

Use tenant ID when account belongs to multiple tenants or CFF resolves wrong tenant.

```powershell
az login --tenant <tenant-id>
cff login
```

Device code + tenant:

```powershell
az login --use-device-code --tenant <tenant-id>
cff login
```

No-subscription tenant:

```powershell
az login --tenant <tenant-id> --allow-no-subscriptions
cff login
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
cff login
```

`cff login` prints credential type, token expiry, and token preview.
