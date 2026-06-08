# Installation

## Requirements

- Windows 10/11
- Microsoft Azure CLI
- Microsoft Fabric access
- `cff.exe` from latest GitHub Release

## Install Azure CLI

```powershell
winget install --exact --id Microsoft.AzureCLI
```

Restart terminal after install.

## Install CFF

1. Download latest `cff.exe` from Releases.
2. Create tools folder:

   ```powershell
   New-Item -ItemType Directory -Path C:\Tools\CFF -Force
   ```

3. Move `cff.exe` into `C:\Tools\CFF`.
4. Add `C:\Tools\CFF` to user PATH.
5. Open new terminal.
6. Verify:

   ```powershell
   cff --help
   ```

## Expiration

Evaluation builds expire on fixed UTC date embedded in `cff.exe`.

When build expires, download latest release and replace old file.

## Optional Hash Check

Download `checksums.txt` from same release and run:

```powershell
Get-FileHash .\cff.exe -Algorithm SHA256
```

Hash must match `checksums.txt`.
