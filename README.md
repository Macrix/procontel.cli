---
Title: "ProconTEL CLI"
github_url: "https://github.com/Macrix/procontel.cli/edit/main/README.md"
Weight: 8
Description: >
  Use the ProconTelCli.exe command line
---

## Table of Contents

1. [Quick introduction](#id-quick-introduction)
2. [Available commands](#id-available-commands)
3. [Container commands](#id-container-commands)
4. [Endpoint commands](#id-endpoint-commands)
5. [Import commands](#id-import-commands)
6. [Plugin commands](#id-plugin-commands)
	* [Installation of new plugin](#id-plugin-commands-install)
	* [Upgrading existing plugin](#id-plugin-commands-upgrade)
7. [Workspace commands](#id-workspace-commands)
8. [Erase all](#id-erase-all)
9. [Avatar comands](#id-avatar-comands)
10. [About CLI](#id-about-cli)
11. [Compose](#id-compose)
12. [Secure connection](#id-secure-connection)
13. [Exit Codes](#id-exit-codes)
 

1.1 List item
List item
 <div id='id-quick-introduction'/>

## 1. Quick introduction
The ProconTelCli  makes it easy to create and manage a ProconTel ecosystem. It already follows our best practices!

<div id='id-available-commands'/>

## 2. Available commands
To list available commands, either run ```.\ProconTelCli.exe``` with no parameters or execute ```.\ProconTelCLI.exe --help```

```csharp
ProconTelCLI is command line interface for managing ProconTEL server. THIS IS AN ALPHA RELEASE, YOU ARE USING IT AT YOUR OWN RISK.

Usage: procontelCLI [options] [command]

Options:
  -?|-h|--help  Show help information

Commands:
  about         Information about CLI
  avatar        Allow user to manage Avatar feature.
  compose       Manage ProconTEL ecosystem by executing yaml strcipt. This is experimental feature!!!
  container     Manage containers (channel or pools) running on ProconTEL server.
  endpoint      Manage endpoints running on ProconTEL server.
  import        Import PEX file.
  plugin        Manage plugins installed on ProconTEL server.
  prune         Completelly erasing all declared ProconTEL workspaces/channel/endpoints and Plugins
  workspace     Manage workspaces running on ProconTEL server.

Run 'procontelCLI [command] --help' for more information about a command.
```

<div id='id-container-commands'/>

## 3. Container commands

Create a pool called TestPool in workspace TestWorkspace
```csharp
.\procontelcli.exe container new -p -w TestWorkspace TestPool
```
<br/>

Create a channel called TestChannel in workspace TestWorkspace
```csharp
.\procontelcli.exe container new -w TestWorkspace TestChannel
```
<br/>

Deletes TestPool
```csharp
.\procontelcli.exe container delete TestPool1
```
<br/>

Activate container(s) TestPool1, TestPool2 [(Not covered by security)](#id-secure-connection)
```csharp
.\procontelcli.exe container activate TestPool1 TestPool2
```
<br/>

Deactivate container(s) TestPool1, TestPool2
```csharp
.\procontelcli.exe container deactivate TestPool1 TestPool2
```
<br/>

Add new dependency between TestPool1 and TestPool2
```csharp
.\procontelcli.exe container dependency create TestPool1 TestPool2
```
<b>Options:</b>
<br/>
Startup delay in [ms]
```csharp
-d or --delay
```
Flag indicating waiting for dependent channels/pools to be fully active
```csharp
-w or --wait
```
Timeout in [ms] for waiting for dependent channels/pools
```csharp
-wt or --wait-timeout
```
<br/>

Get details about container
```csharp
.\procontelcli.exe container describe TestPool
```
<br/>

List containers
```csharp
.\procontelcli.exe container list
```
<b>Options:</b>
<br/>
Container type (All, Pool, Channel)
```csharp
-c or --container
```

to be continued...
<div id='id-endpoint-commands'/>

## 4. Endpoint commands

Create new endpoint called TestEndpoint in the channel called TestChannel from TestPlugin plugin on localhost
```csharp
.\procontelcli.exe endpoint new -c TestChannel -p TestPlugin.Endpoint@TestPlugin -s localhost
```
One remark: this: <b>TestPlugin.Endpoint@TestPlugin</b> hopefully will be replaced by something better in the newer version of ProcontelCLI. It's built as namespace of endpoint class @ name of plugin.

<br/>

Display list of endpoints running on TestChannel
```csharp
.\procontelcli.exe endpoint list TestChannel -s localhost:9000
```
<br/>

Display parameters of endpoint called TestEndpoint
```csharp
.\procontelcli.exe endpoint params TestEndpoint -s localhost:9000
```
<br/>

Update parameter ActsAsProvider to ```true``` of endpoint called TestEndpoint
```csharp
.\procontelcli.exe endpoint params TestEndpoint -u="ActsAsProvider=true" -s localhost:9000
```
<br/>

Display internal configuration of endpoint called TestEndpoint
```csharp
.\procontelcli.exe endpoint config TestEndpoint -s localhost:9000
```
<br/>

Update internal configuration to ```CONFIGURATION_VALUE``` of endpoint called TestEndpoint
```csharp
.\procontelcli.exe endpoint config TestEndpoint -u="CONFIGURATION_VALUE" -s localhost:9000
```
<br/>

Load internal configuration from local file ```C:\configuration.txt``` of endpoint called TestEndpoint
```csharp
.\procontelcli.exe endpoint config TestEndpoint -f="C:\configuration.txt" -s localhost:9000
```
<br/>

Replace xml internal configuration property of endpoint called TestEndpoint
```csharp
.\procontelcli.exe endpoint config TestEndpoint -r-xml="PluginConfiguration/MethodName=NEW_VALUE" -s localhost:9000
```
<br/>

Replace json internal configuration property of endpoint called TestEndpoint
```csharp
.\procontelcli.exe endpoint config TestEndpoint -r-json="PluginConfiguration.MethodName=NEW_VALUE" -s localhost:9000
```
<br/>

Activate endpoint(s) TestEndpoint1, TestEndpoint2
```csharp
.\procontelcli.exe endpoint activate TestEndpoint1 TestEndpoint2 -s localhost:9000
```
<br/>

Dectivate endpoint(s) TestEndpoint1, TestEndpoint2
```csharp
.\procontelcli.exe endpoint deactivate TestEndpoint1 TestEndpoint2 -s localhost:9000
```
<br/>

Deletes endpoint TestEndpoint
```csharp
.\procontelcli.exe endpoint delete TestEndpoint1 -s localhost:9000
```
<b>Options:</b>
<br/>
Container name
```csharp
-c or --container
```

Get details about TestEndpoint
```csharp
.\procontelcli.exe endpoint describe TestEndpoint -s localhost:9000
```
<br/>

to be continued...
<div id='id-import-commands'/>

## 5. Import commands
Import PEX file from path 'c:\testfolder\test_import.pex'
```csharp
.\procontelcli.exe import c:\testfolder\test_import.pex
```
<b>Options:</b>
<br/>
Import also plugins
```csharp
-p or --with-plugins
```
Clean import
```csharp
-c or --clean
```
<br/>

to be continued...

<div id='id-plugin-commands'/>

## 6. Plugin commands

<div id='id-plugin-commands-install'/>
<br/>

### Installation of new plugin
<br/>

Install plugin called Test Plugin 
```csharp
.\procontelcli.exe plugin install D:\SampleProject\TestPlugin.dll
```
<br/>

Install plugin called Test Plugin with dependent an additional dll binaries 
```csharp
.\procontelcli.exe plugin install D:\SampleProject\TestPlugin.dll -f D:\SampleProject\contrib\|*.dll||R
```
Where 'R' is a flag to search for defined files recursively in mentioned path

</br>

Install plugin called Test Plugin with dependent an additional dll binaries from two directories
(additional directories require adding next -f parameter)
```csharp
.\procontelcli.exe plugin install D:\SampleProject\TestPlugin.dll -f D:\SampleProject\contrib\|*.dll||R -f D:\SampleProject\additionalLibs\|*.dll||R
```
<br/>

Get information about installed plugin
```csharp
.\ProconTelCLI.exe plugin describe ExampleTelegramEndpoint
Plugin:
  FullName: ExampleTelegramEndpoint, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null
  Version: 1.0.0.0
  UpdateDate: 2021-03-23 12:33:59
  InstallDate: 2021-03-19 09:41:45
```
<br/>

<div id='id-plugin-commands-upgrade'/>

### Upgrading existing plugin
<br/>

There is also possibillity to upgrade existing, already installed, plugins by using command
```
.\ProconTelCLI.exe plugin upgrade PluginName
```
 or even few plugins at the same time
 ```
.\ProconTelCLI.exe plugin upgrade PluginName AnotherPluginName AdditionalPluginName
```

There is also option to upgrade all installed plugins in simple way:
```
.\ProconTelCLI.exe plugin upgrade *
```
The `*` character can be used only alone, i.e.
```
.\ProconTelCLI.exe plugin upgrade ExampleTelegramEndpoint *
```
is illegal, the `*` character will be filter out and only names will be processing

<br/>

<div id='id-workspace-commands'/>

## 7. Workspace commands
Create new workspace called TestWorkspace
```csharp
.\procontelcli.exe workspace new TestWorkspace
```
<br/>

Remove workspace called TestWorkspace
```csharp
.\procontelcli.exe workspace delete TestWorkspace
```
<br/>

Activate workspace(s) TestWorkspace1, TestWorkspace2
```csharp
.\procontelcli.exe workspace activate TestWorkspace1 TestWorkspace2
```
<br/>

Deactivate workspace(s) TestWorkspace1, TestWorkspace2
```csharp
.\procontelcli.exe workspace deactivate TestWorkspace1 TestWorkspace2
```
<br/>

Get all workspaces
```csharp
.\procontelcli.exe workspace list
```
<br/>

<div id='id-erase-all'/>

## 8. Erase all

Completelly erasing all declared ProconTEL workspaces/channel/endpoints and Plugins
```csharp
.\procontelcli.exe prune
```
<br/>

<div id='id-avatar-comands'/>

## 9. Avatar comands

Create Avatar for TestEndpoint inside of TestChannel
```csharp
.\procontelcli.exe avatar create TestEndpoint TestChannel
```
<b>Options:</b>
<br/>
Source avatar address
```csharp
-a or --address
```
<br/>

Delete Avatar for TestEndpoint inside of TestChannel
```csharp
.\procontelcli.exe avatar delete TestEndpoint TestChannel
```
<br/>

Get list of Avatars in TestChannel
```csharp
.\procontelcli.exe avatar list TestChannel
```
<br/>

<div id='id-about-cli'/>

## 10. About CLI

Get version of CLI [(Not covered by security)](#id-secure-connection)
```csharp
.\procontelcli.exe about version
```
<br/>

<div id='id-compose'/>

## 11. Compose

Execute yaml strcipt. This is experimental feature!!! Compose script file path
```csharp
.\procontelcli.exe compose up C:\script.yaml
```
<br/>

<div id='id-secure-connection'/>

## 12. Secure connection

If the ProconTel is secured with password and/or certificate, the CLI is still able to work, but need some additional parameters to be set up. For example command below will not be executed if there are security features turned on:
```
.\ProconTelCLI.exe  container new exampleContainer 
```

but code below, with additional security parameters, will work fine 
```
.\ProconTelCLI.exe  container new exampleContainer --certificate client-certificate --certificateStorage TrustedPeople --password test 
```

There are 4 security parameters which can be used in CLI:
1. `--certificate` - specify the name of certificate used to sign communication with ProconTel api
2. `--certificateStorage` - specify the place where certificate is store, i.e. _Personal_, _TrustedPeople_...  
3. `--revocationMode` - specify the revocation mode for secure communication, it supports following options _NoCheck_, _Online_, _Offline_ 
4. `--password` - here is specified a password for establishing connection

`--password` and three other parameters can be used separately i.e. in case when you have specified certificates only the password is not required. For establishing communication with server secured by certificate `--certificate` and `--certificateStorage` parameters are mandatrory, the `--revocationMode` is optional (by default is used _NoCheck_).

<br/>

<div id='id-exit-codes'/>

## 13. Exit codes

Global exit codes
| Exit Code | Description |
| :---: | :---: |
| 0 | Success |
| 1 | Incorrect Command |
| 2 | Command Failure |

<br/>
Specific exit codes and description

| Exit Code | Description |
| :---: | :---: |
| 100 | Endpoint deos not exist |
| 101 | Container does not exist |
| 102 | Workspace does not exist |
| 103 | Plugin does not exist |
| 104 | Dependency does not exist |
| 105 | Destination container already contain avatar of selected endpoint |
| 106 | Destination container cannot be pool |
| 107 | Container is active |
| 108 | No avatar in container |
| 109 | No endpoint in container |
| 110 | Transfering plugin files failed |
| 111 | Upgrading plugin failed |
| 112 | Plugin validation failed |
| 113 | Pool cannot contain avatar |
| 114 | Wrong container type |

<br/>

to be continued...