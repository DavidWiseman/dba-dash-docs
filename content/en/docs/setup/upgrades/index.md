---
title: "Upgrades"
description: "Upgrade DBA Dash to latest version"
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
images: []
menu:
  docs:
    parent: "setup"
weight: 120
toc: true
---
## Prerequisites

* Consider backing up your DBA Dash repository database and ServiceConfig.json file from the installation folder.
## How to upgrade

1. Open the DBA Dash service configuration tool
2. Click check for updates
3. If an upgrade is available click "Upgrade"
4. A powershell script will run that will perform the upgrade.  

{{< alert icon="ℹ️" text="It might take a few minutes to shutdown the DBA Dash service as it waits for collections to complete.  Starting the service could also take a few minutes as it upgrades the DBA Dash repository database and starts up the collections" />}}

## Upgrading GUI clients

1. The GUI will automatically prompt to upgrade on startup if the version is older than the repository database.
   
{{< alert icon="ℹ️" text="The client will only be prompted for upgrade if the x.y portion of the x.y.z version is different from the repository database." />}}

1. Click Help, About to check the version of the client
2. Click Upgrade to upgrade.


---
## Manual upgrade

There might be situations where you need to perform an upgrade manually.  e.g. The server doesn't have any internet connectivity.

1. Download the latest release
2. Stop the DBA Dash service (using the service configuration tool, services.msc or `net stop DBADashService`)
3. Close all instances of the GUI or service configuration tool that are running.
4. Extract the contents of the downloaded zip to replace the existing installation files.

{{< alert icon="ℹ️" text="The ServiceConfig.json file is the only file you need to keep.  This contains all the settings for the service. If you created PerformanceCountersCustom.xml you should also keep this file." />}}

## Command line Upgrade

```cmd
DBADashConfig -a Update
```

Or (Supported on old versions of DBA Dash):

```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
Invoke-WebRequest -Uri https://raw.githubusercontent.com/trimble-oss/dba-dash/main/Scripts/UpgradeDBADash.ps1 -OutFile UpgradeDBADash.ps1
./UpgradeDBADash.ps1
```

For a specific version:
```powershell
./UpgradeDBADash.ps1 -Tag 2.22.0
```