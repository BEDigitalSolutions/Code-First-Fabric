# Usage

## Help

```powershell
cff --help
cff <command> --help
cff --help --json
cff <command> --help --json
```

Use `--json` with help when an agent or script needs machine-readable command metadata.

## Auth and Discovery

```powershell
cff login
cff list workspaces
cff list workspaces --json
```

`cff login` verifies the current credential and prints token metadata. `cff list workspaces` lists visible Fabric workspaces, sorted by `displayName`. It prints a table by default; `--json` prints structured output.

List items in a workspace:

```powershell
cff list artifacts "<workspace-name-or-id>"
cff list artifacts "<workspace-name-or-id>" --json
```

Include Fabric folder paths and sort by path:

```powershell
cff list artifacts "<workspace-name-or-id>" --paths
```

Filter artifacts by canonical Fabric item type:

```powershell
cff list artifacts "<workspace-name-or-id>" --type DataPipeline
cff list artifacts "<workspace-name-or-id>" --paths --type=Notebook
```

`--type` is case-insensitive, but it expects canonical Fabric type names such as `DataPipeline`, `Notebook`, `Lakehouse`, `Warehouse`, `VariableLibrary`, or `SemanticModel`. Dashed aliases such as `data-pipeline` are not accepted.

List item types present in a workspace:

```powershell
cff list types "<workspace-name-or-id>"
cff list types "<workspace-name-or-id>" --json
```

List item job instances:

```powershell
cff list jobs "<workspace-name-or-id>"
cff list jobs "<workspace-name-or-id>" 2026-06-01 2026-06-26
cff list jobs "<workspace-name-or-id>" --type DataPipeline --json
```

With no dates, `list jobs` scans the last 24 hours. With one date, it scans from that date to now. With two dates, it scans the inclusive range. Date values can be `YYYY-MM-DD` or ISO-style UTC timestamps. Known job history sources include Fabric job instances for `DataPipeline` and `Notebook`, plus Power BI refresh history for model-based `SemanticModel` items.

List enabled schedules:

```powershell
cff list schedules "<workspace-name-or-id>"
cff list schedules "<workspace-name-or-id>" --type Notebook
cff list schedules "<workspace-name-or-id>" --json
```

Known schedule sources include Fabric item schedules for `DataPipeline` and `Notebook`, plus Power BI refresh schedules for model-based `SemanticModel` items. Unsupported type filters return warnings instead of silently guessing.

## Configuration

Show, set, or reset the pull-history storage path:

```powershell
cff config hist-path
cff config hist-path C:\CFF\history
cff config hist-path --reset
```

`pull` stores raw Fabric definitions in pull history. Choose a secure location because definitions may contain secrets or sensitive configuration.

## Workspace Sync

`pull` and `push` are the core Code First Fabric workflow. Use them when you want a Fabric workspace represented as local files, then want to send local changes back to Fabric.

Before pulling into an existing folder, review any local changes you care about. `pull` writes Fabric artifact files into the output tree and records raw pull history.

Before pushing, remember that `push` creates missing folders/items, updates existing item metadata and definitions, recreates moved items, maps local logical IDs back to real remote IDs, patches notebook Lakehouse references, and converts Jupyter notebooks to Fabric source before upload.

Workspace sync supports `Lakehouse`, `Warehouse`, `DataPipeline`, `Notebook`, and `VariableLibrary` item definitions.

Pull Fabric artifacts into a local folder:

```powershell
cff pull "<workspace-name-or-id>" .\fabric-source
```

Pull one Fabric item or folder subtree:

```powershell
cff pull "<workspace-name-or-id>" .\fabric-source "Folder/NotebookName.Notebook"
```

Use local paths under the output folder to target existing pulled items:

```powershell
cff pull "<workspace-name-or-id>" .\fabric-source .\fabric-source\Folder\NotebookName.Notebook
```

Tune pull definition downloads or print timing details:

```powershell
cff pull "<workspace-name-or-id>" .\fabric-source --definition-concurrency 8 --time
```

Push local artifacts into a workspace:

```powershell
cff push "<workspace-name-or-id>" .\fabric-source
```

Push one local item folder or a file inside an item:

```powershell
cff push "<workspace-name-or-id>" .\fabric-source "Folder/NotebookName.Notebook"
cff push "<workspace-name-or-id>" .\fabric-source .\fabric-source\Folder\NotebookName.Notebook\notebook-content.ipynb
```

Create missing workspace folders and items from a local tree without the full update flow:

```powershell
cff upload-workspace "<workspace-name-or-id>" .\fabric-source
```

Update one pulled notebook definition using the notebook folder metadata:

```powershell
cff update-notebook .\fabric-source\Folder\NotebookName.Notebook
```

If no notebook directory is passed, `update-notebook` uses the current directory.

## Push and Run Pipeline

Push dependencies and a data pipeline from a local workspace copy, then run the pipeline:

```powershell
cff push-run-pipeline "<workspace-name-or-id>" .\fabric-source "PipelineName" "[NotebookA, LakehouseA]"
```

Use an empty dependency list when only the pipeline should be pushed before running:

```powershell
cff push-run-pipeline "<workspace-name-or-id>" .\fabric-source "PipelineName" "[]"
```

Collect full diagnostics for the run:

```powershell
cff push-run-pipeline "<workspace-name-or-id>" .\fabric-source "PipelineName" "[NotebookA]" --diagnose --output-dir .\diagnostics --output-file run.json
```

Dependencies are local artifact display names. The pipeline must be a `DataPipeline` artifact.

## Lakehouse Files

Download a file or folder from Lakehouse `Files/`:

```powershell
cff download-lakehouse-files "<workspace-name-or-id>" "<lakehouse-name-or-id>" "remote/path" .\downloads
```

Upload a file or folder into Lakehouse `Files/`:

```powershell
cff upload-lakehouse-files "<workspace-name-or-id>" "<lakehouse-name-or-id>" .\local-file.txt "remote/path"
```

The remote path is relative to the Lakehouse `Files/` area.

## SQL

Run inline SQL against a Lakehouse SQL endpoint or Warehouse:

```powershell
cff sql run query "<workspace-name-or-id>" lakehouse "<lakehouse-name-or-id>" "select 1"
cff sql run query "<workspace-name-or-id>" warehouse "<warehouse-name-or-id>" "select 1"
```

Run SQL from a file:

```powershell
cff sql run file "<workspace-name-or-id>" lakehouse "<lakehouse-name-or-id>" .\query.sql
cff sql run file "<workspace-name-or-id>" warehouse "<warehouse-name-or-id>" .\query.sql
```

Print SQL connection metadata without running SQL:

```powershell
cff sql endpoint "<workspace-name-or-id>" lakehouse "<lakehouse-name-or-id>"
cff sql endpoint "<workspace-name-or-id>" warehouse "<warehouse-name-or-id>"
```

Run smoke checks against one Lakehouse and one Warehouse:

```powershell
cff sql smoke "<workspace-name-or-id>" "<lakehouse-name-or-id>" "<warehouse-name-or-id>"
```

SQL commands print JSON with the resolved target and statement results.

## Schema Pull

Pull schema for one item:

```powershell
cff pull-schema item "<workspace-name-or-id>" "<item-name-or-id>" .\schema lakehouse
cff pull-schema item "<workspace-name-or-id>" "<item-name-or-id>" .\schema --type warehouse
```

Pull schema for all Lakehouses and Warehouses in a workspace:

```powershell
cff pull-schema workspace "<workspace-name-or-id>" .\schema
```

Schema output is written as `.sql` files and includes table/view counts and schema names.

## Livy

Run a Python script or notebook file in a Fabric Lakehouse Livy session:

```powershell
cff livy run-file "<workspace-name-or-id>" "<lakehouse-name-or-id>" .\script.py
cff livy run-file "<workspace-name-or-id>" "<lakehouse-name-or-id>" .\notebook.ipynb --session-name cff-dev --timeout-seconds 900
```

Optional flags include `--session-name`, `--environment-id`, and `--timeout-seconds`.

## Diagnostics

Diagnose a pipeline job:

```powershell
cff diagnose "<workspace-name-or-id>" "<job-id>" .\diagnostics
```

Choose the diagnostics output file name:

```powershell
cff diagnose "<workspace-name-or-id>" "<job-id>" .\diagnostics --output-file job.json
```

Diagnostics query activity runs for the pipeline job, write full activity JSON, and print a filtered failure summary for pipeline, notebook, and SQL stored procedure activities.
