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

Code First Fabric currently pulls and pushes these Microsoft Fabric item types as local folders/files:

- `Lakehouse`
- `Warehouse`
- `DataPipeline`
- `Notebook`
- `Report`
- `SemanticModel`
- `VariableLibrary`
- `GraphModel`
- `Ontology`

Reports use `PBIR` definitions. Semantic Models use `TMDL` definitions. Lakehouse `Files/` content is handled by dedicated upload/download commands.

It also includes commands for workspace discovery, Lakehouse `Files/` upload/download, SQL endpoints, schema export, Livy execution, pipeline diagnostics, job/schedule inspection, HTML job reports, a local Fabric monitor, and telemetry controls.

## Typical Workflows

### 🚀 AI Agent Workflow

**YOU + AI + CFF: BUILD FASTER. BUILD BETTER.**

AI coding agents excel at working with Microsoft Fabric through Code First Fabric on both greenfield and brownfield projects.

The coding agent seamlessly creates and modifies Fabric artifacts at your convenience.

**1. Sign in with the Azure CLI**

In your terminal:

```
az login
```

**2. Open your preferred IDE and AI coding agent**

Compatible with any IDE (VS Code, Cursor, Terminal, etc.) and any coding agent (GPT, Claude, Gemini, Qwen, Kimi, etc.).

Prompt your preferred coding agent to explore the CLI:

```
cff --help
```

**3. Start the revolution**

Prompt your agent to get a specific workspace:

```
Get the following Fabric workspace: [workspace-name]
```

**Enjoy a smooth, collaborative workflow between you, your AI agent, and Microsoft Fabric.**

**The sky is the limit! 🚀**


### Terminal Workflow

**1. Install CFF**

Follow the [installation guide](docs/installation.md) to download `cff.exe` and add it to your PATH.

**2. Sign in and start working**

Sign in with Azure CLI, then start from a Fabric workspace you can access.

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
| [Configuration](docs/configuration.md) | Azure CLI login, tenant-specific login, device-code login, service principal auth, and shared CFF storage. |
| [Usage](docs/usage.md) | Command examples for discovery, sync, SQL, schema, Lakehouse files, Livy, monitor, telemetry, pipeline runs, jobs, schedules, HTML reports, and diagnostics. |
| [Troubleshooting](docs/troubleshooting.md) | Common setup, login, PATH, optional expiry, storage migration, monitor, and hash-check issues. |
| [Telemetry Privacy Notice](docs/Aviso-privacidad-telemetria.md) | Privacy information for telemetry-enabled releases. |

## File Integrity

Releases can include `checksums.txt` with SHA256 hashes. To verify a downloaded executable:

```powershell
Get-FileHash .\cff.exe -Algorithm SHA256
```

Compare the result with `checksums.txt` from the same release.
