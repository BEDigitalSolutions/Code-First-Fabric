# Code First Fabric

A command-line interface CLI to code in the Microsoft Fabric infrastructure.

Build on Fabric as a real data engineer should; use your terminal, your Git, your IDE (VS Code, T3, Cursor...), and your coding agents (Codex, Claude Code, Gemini, Deep Seek, Copilot...).

## Installation

Code First Fabric is distributed as a Windows executable named `cff.exe`.

Download the latest release, put `cff.exe` in a folder on your PATH, install Microsoft Azure CLI, and verify with `cff --help`.

Full installation steps are in [docs/installation.md](docs/installation.md).

Click [here](https://github.com/BEDigitalSolutions/Code-First-Fabric/releases/download/v2026.07.31/cff.exe) to download CFF CLI.

## Why Use It

Microsoft Fabric is a powerful infrastructure, but day-to-day engineering work often needs much more than a browser UI.

Fully coded development, testing, debugging, reviewing, deployment, and replication of Fabric projects.

- Give coding agents a CLI and full context for Fabric engineering tasks.
- Keep your Fabric artifacts in a local environment.
- Code, run and debug Python, notebooks and pipelines from your terminal.
- Use Git diffs and pull requests for Fabric changes.
- Push artifacts or full workspaces back to Fabric.
- Run SQL and schema checks from the terminal.
- Upload and download Lakehouse files content.
- Push dependencies, run Fabric data pipelines, and collect diagnostics.
- Inspect workspace jobs and schedules, monitor pipeline failures, and collect activity-run evidence quickly.

## Supported Fabric Items

Code First Fabric currently pulls, pushes, and uploads these Microsoft Fabric item types as local files:

- `Lakehouse`
- `Warehouse`
- `DataPipeline`
- `Notebook`
- `VariableLibrary`

It also includes commands for workspace discovery, Lakehouse `Files/` upload/download, SQL endpoints, schema export, Livy execution, pipeline diagnostics, and job/schedule inspection.

## Typical Workflow

Install `cff.exe`, sign in with Azure CLI, then start from a Fabric workspace you can access.

```powershell
az login
cff --help
cff list workspaces
cff list artifacts "<workspace-name>" --paths
cff pull "<workspace-name>" .\your-local-path

> "Start coding now!"

cff push "<workspace-name>" .\your-local-path
```

For exact command syntax and examples, see [docs/usage.md](docs/usage.md).

## Build Expiration

Current builds can be permanent or built with an optional UTC expiration date. If an expiring build is used, `cff.exe` exits with a clear expiry message on or after its cutoff date.

When a build expires, download the latest release and replace the old `cff.exe`.

## Documentation

| Document | Purpose |
|---|---|
| [Installation](docs/installation.md) | Download `cff.exe`, install Azure CLI, set PATH, verify the executable. |
| [Configuration](docs/configuration.md) | Azure CLI login, tenant-specific login, device-code login, service principal auth, and pull history path. |
| [Usage](docs/usage.md) | Command examples for discovery, sync, SQL, schema, Lakehouse files, Livy, pipeline runs, jobs, schedules, and diagnostics. |
| [Troubleshooting](docs/troubleshooting.md) | Common setup, login, PATH, optional expiry, pull history, and hash-check issues. |

## File Integrity

Releases can include `checksums.txt` with SHA256 hashes. To verify a downloaded executable:

```powershell
Get-FileHash .\cff.exe -Algorithm SHA256
```

Compare the result with `checksums.txt` from the same release.
