# Installation

Code First Fabric is distributed to users as a Windows executable named `cff.exe`.

## Requirements

- Windows 10/11
- Microsoft Azure CLI
- Microsoft Fabric access
- `cff.exe` from the latest GitHub Release

## 1. Download CFF

Download `cff.exe` from the latest GitHub Release:

https://github.com/BEDigitalSolutions/Code-First-Fabric/releases

## 2. Install CFF

Create a tools folder and copy `cff.exe` into it:

```powershell
New-Item -ItemType Directory -Path C:\Tools\CFF -Force
Copy-Item .\cff.exe C:\Tools\CFF\cff.exe -Force
```

Add `C:\Tools\CFF` to your user PATH:

```powershell
$dir = "C:\Tools\CFF"
$userPath = [Environment]::GetEnvironmentVariable("Path", "User")
if (($userPath -split ";") -notcontains $dir) {
  [Environment]::SetEnvironmentVariable("Path", "$userPath;$dir", "User")
}
$env:Path += ";$dir"
```

Verify the executable:

```powershell
cff --help
```

If `cff` is not found, open a new terminal. If using VS Code, restart VS Code too.

## 3. Install Azure CLI

Code First Fabric uses Azure CLI credentials by default.

```powershell
winget install --exact --id Microsoft.AzureCLI
```

Restart your terminal after installing Azure CLI.

## 4. Sign In

Use Azure CLI for the normal interactive login flow:

```powershell
az login
cff login
```

If your tenant has no Azure subscriptions, use:

```powershell
az login --allow-no-subscriptions
cff login
```

More login options, including device-code login, tenant-specific login, and service principal authentication, are documented in [configuration.md](configuration.md).

## 5. Start Using CFF

List visible Fabric workspaces:

```powershell
cff list workspaces
```

Pull a workspace into a local folder:

```powershell
cff pull "<workspace-name>" .\fabric-source
```

For command examples, see [usage.md](usage.md).

## Shell Completion

When run in an interactive terminal, `cff` may install shell completion hooks for supported shells and print a message asking you to restart the terminal.

You can also print a completion script manually:

```powershell
cff completion powershell
```

Supported shells are `powershell`, `bash`, `zsh`, and `fish`.

## Build Expiration

Current public builds are evaluation builds with a fixed UTC expiration date embedded in `cff.exe`.

The current build expires on `2026-07-31` at `00:00 UTC`.

1. Download the latest `cff.exe` from Releases.
2. Replace the old file in your PATH folder.
3. Open a new terminal.
4. Run `cff --help`.

## Optional Hash Check

Each release can include `checksums.txt`. Download it from the same release and run:

```powershell
Get-FileHash .\cff.exe -Algorithm SHA256
```

Compare the hash with `checksums.txt`.

## Related Docs

- [Configuration](configuration.md)
- [Usage](usage.md)
- [Troubleshooting](troubleshooting.md)
