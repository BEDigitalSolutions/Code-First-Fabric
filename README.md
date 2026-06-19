# Code First Fabric

Code First Fabric is a command-line tool for data engineers who want to work with Microsoft Fabric from local files, Git, editors, terminals, and automated workflows.

It lets you pull supported Fabric workspace artifacts into a local source tree, inspect and change them like code, push updates back to Fabric, run validation queries, move Lakehouse files, and diagnose failed pipeline runs without jumping between disconnected screens.

## Why Use It

Microsoft Fabric is powerful, but day-to-day engineering work often needs more than a browser UI. Code First Fabric helps make Fabric projects easier to develop, test, debug, review, and repeat.

- Keep Fabric artifacts in a local folder structure that is easier to inspect and compare.
- Use Git diffs and pull requests for Fabric changes.
- Edit notebooks as standard Jupyter `.ipynb` files.
- Push selected artifacts or full workspace trees back to Fabric.
- Run SQL and schema checks from the terminal.
- Upload and download Lakehouse `Files/` content through OneLake.
- Run Python or notebooks in Fabric Lakehouse Livy sessions.
- Diagnose pipeline failures and collect activity-run evidence quickly.
- Give coding agents a concrete CLI for Fabric engineering tasks.

## What It Works With

Code First Fabric currently focuses on these Microsoft Fabric item types:

- `Lakehouse`
- `DataPipeline`
- `Notebook`
- `VariableLibrary`
- `Warehouse`

It also works with Lakehouse `Files/`, Fabric SQL endpoints, Livy sessions, and pipeline job diagnostics.

## Typical Workflow

Install `cff.exe`, sign in with Azure CLI, then start from a Fabric workspace you can access.

```powershell
az login
cff list-workspaces
cff pull "<workspace-name>" .\fabric-source
cff push "<workspace-name>" .\fabric-source
```

For exact command syntax and examples, see [docs/usage.md](docs/usage.md).

## Installation

Code First Fabric is distributed as a Windows executable named `cff.exe`.

Download the latest release, put `cff.exe` in a folder on your PATH, install Microsoft Azure CLI, and verify with `cff --help`.

Full installation steps are in [docs/installation.md](docs/installation.md).

## Evaluation Build

The current public build is an evaluation build and expires on `2026-07-31` at `00:00 UTC`.

When it expires, download the latest release and replace the old `cff.exe`. Future stable licensed builds are expected to change this distribution model.

## Documentation

| Document | Purpose |
|---|---|
| [Installation](docs/installation.md) | Download `cff.exe`, install Azure CLI, set PATH, verify the executable. |
| [Configuration](docs/configuration.md) | Azure CLI login, tenant-specific login, device-code login, and service principal auth. |
| [Usage](docs/usage.md) | Command examples for sync, SQL, schema, Lakehouse files, Livy, and diagnostics. |
| [Troubleshooting](docs/troubleshooting.md) | Common setup, login, PATH, expiry, and hash-check issues. |

## File Integrity

Releases can include `checksums.txt` with SHA256 hashes. To verify a downloaded executable:

```powershell
Get-FileHash .\cff.exe -Algorithm SHA256
```

Compare the result with `checksums.txt` from the same release.
