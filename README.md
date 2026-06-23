# Code First Fabric

A command-line interface CLI to code in the Microsoft Fabric infrastructure.

Build on Fabric as a real data engineer should; use your terminal, your Git, your IDE (VS Code, T3, Cursor...), and your coding agents (Codex, Claude Code, Gemini, Deep Seek, Copilot...).

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
- Monitor pipeline failures and collect activity-run evidence quickly.

## Supported Artifacts

Code First Fabric currently supports these Microsoft Fabric item types:

- `Lakehouse`
- `Warehouse`
- `Lakehouse files`
- `SQL endpoints`
- `DataPipeline`
- `Notebook`
- `VariableLibrary`

## Typical Workflow

Install `cff.exe`, sign in with Azure CLI, then start from a Fabric workspace you can access.

```powershell
az login
cff --help
cff list workspaces
cff pull "<workspace-name>" .\your-local-path

> "Start coding now!"

cff push "<workspace-name>" .\your-local-path
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
| [Configuration](docs/configuration.md) | Azure CLI login, tenant-specific login, device-code login, service principal auth, and pull history path. |
| [Usage](docs/usage.md) | Command examples for sync, SQL, schema, Lakehouse files, Livy, pipeline runs, and diagnostics. |
| [Troubleshooting](docs/troubleshooting.md) | Common setup, login, PATH, expiry, pull history, and hash-check issues. |

## File Integrity

Releases can include `checksums.txt` with SHA256 hashes. To verify a downloaded executable:

```powershell
Get-FileHash .\cff.exe -Algorithm SHA256
```

Compare the result with `checksums.txt` from the same release.
