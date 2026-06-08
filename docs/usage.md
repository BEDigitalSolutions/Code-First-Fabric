# Usage

## Help

```powershell
cff --help
```

## Auth and Discovery

```powershell
cff login
cff list-workspaces
```

## Workspace Sync

Pull Fabric artifacts into local folder:

```powershell
cff pull "<workspace-name>" .\fabric-source
```

Push local artifacts into workspace:

```powershell
cff push "<workspace-name>" .\fabric-source
```

Upload missing workspace artifacts:

```powershell
cff upload-workspace "<workspace-name>" .\fabric-source
```

Update one notebook definition:

```powershell
cff update-notebook .\fabric-source\notebook-folder
```

## Lakehouse Files

Download file or folder from Lakehouse `Files/`:

```powershell
cff pull-lakehouse-files "<workspace-name>" "<lakehouse-name>" "remote/path" .\downloads
```

Upload file or folder into Lakehouse `Files/`:

```powershell
cff upload-lakehouse-files "<workspace-name>" "<lakehouse-name>" .\local-file.txt "remote/path"
```

## SQL

Lakehouse SQL:

```powershell
cff sql-lakehouse run "<workspace-name>" "<lakehouse-name>" "select 1"
cff sql-lakehouse run-file "<workspace-name>" "<lakehouse-name>" .\query.sql
cff sql-lakehouse endpoint-name "<workspace-name>" "<lakehouse-name>"
```

Warehouse SQL:

```powershell
cff sql-warehouse run "<workspace-name>" "<warehouse-name>" "select 1"
cff sql-warehouse run-file "<workspace-name>" "<warehouse-name>" .\query.sql
cff sql-warehouse endpoint-name "<workspace-name>" "<warehouse-name>"
```

Unified workspace SQL:

```powershell
cff sql-workspace run "<workspace-name>" lakehouse "<lakehouse-name>" "select 1"
cff sql-workspace run "<workspace-name>" warehouse "<warehouse-name>" "select 1"
```

## Schema Pull

Pull schema for one item:

```powershell
cff schema-pull item "<workspace-name>" "<item-name>" .\schema lakehouse
```

Pull schema for workspace:

```powershell
cff schema-pull workspace "<workspace-name>" .\schema
```

## Livy

Run Python or notebook file in Lakehouse Livy session:

```powershell
cff livy run-file "<workspace-name>" "<lakehouse-name>" .\script.py
```

## Diagnostics

Diagnose pipeline job:

```powershell
cff diagnose "<workspace-name>" "<job-id>" .\diagnostics
```
