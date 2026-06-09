# Code First Fabric

Code First Fabric (CFF) is a Windows command-line tool for working with Microsoft Fabric artifacts as code.

This public distribution contains evaluation builds of `cff.exe`, plus installation, configuration, and usage documentation.

## Evaluation Build

Current build expires on `2026-07-31` at `00:00 UTC`.

After expiration, download latest release and replace old `cff.exe`.

## Requirements

- Windows 10/11
- Microsoft Azure CLI
- Access to a Microsoft Fabric tenant and workspace
- Microsoft Fabric permissions for target workspaces

## Installation

1. Download latest `cff.exe` from Releases or by clicking [here](https://github.com/BEDigitalSolutions/Code-First-Fabric/releases/download/v2026.07.31/cff.exe)
2. Move `cff.exe` to a folder in your PATH, or run the following command in terminal:

   ```powershell
   New-Item -ItemType Directory -Path C:\Tools\CFF -Force
   Copy-Item .\cff.exe C:\Tools\CFF\cff.exe -Force
   cff --help
   ```

3. Install Azure CLI by running the following command in terminal:

   ```powershell
   winget install --exact --id Microsoft.AzureCLI
   ```

4. Restart terminal.
5. Verify install:

   ```powershell
   cff --help
   ```

Full steps: [docs/installation.md](docs/installation.md)

## Authentication

Default login:

```powershell
az login
```

Tenant has no Azure subscriptions:

```powershell
az login --allow-no-subscriptions
```

Browser login blocked or remote shell:

```powershell
az login --use-device-code
```

Force tenant:

```powershell
az login --tenant <tenant-id>
```

Device code + tenant:

```powershell
az login --use-device-code --tenant <tenant-id>
```

Full auth notes: [docs/configuration.md](docs/configuration.md)

## Common Commands

List workspaces:

```powershell
cff list-workspaces
```

Pull workspace artifacts:

```powershell
cff pull "<workspace-name>" .\fabric-source
```

Push local artifacts:

```powershell
cff push "<workspace-name>" .\fabric-source
```

Run SQL against Lakehouse:

```powershell
cff sql-lakehouse run "<workspace-name>" "<lakehouse-name>" "select 1"
```

Download Lakehouse Files content:

```powershell
cff pull-lakehouse-files "<workspace-name>" "<lakehouse-name>" "path/in/Files" .\downloads
```

Upload Lakehouse Files content:

```powershell
cff upload-lakehouse-files "<workspace-name>" "<lakehouse-name>" .\local-file.txt "target/path"
```

Full usage: [docs/usage.md](docs/usage.md)

## Updating

When build expires:

1. Download latest `cff.exe` from Releases.
2. Replace old `cff.exe`.
3. Run `cff --help`.

## File Integrity

Each release can include `checksums.txt` with SHA256 hashes for release files.

Verify downloaded executable:

```powershell
Get-FileHash .\cff.exe -Algorithm SHA256
```

Compare result with `checksums.txt` from same release.

## Troubleshooting

See [docs/troubleshooting.md](docs/troubleshooting.md).
