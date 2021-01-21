# Use the ProconTelCli.exe command line

## Table of Contents

1. [Quick introduction](#id-quick-introduction)
2. [Available commands](#id-available-commands)
3. [Container commands](#id-container-commands)
4. [Endpoint commands](#id-endpoint-commands)
5. [Import commands](#id-import-commands)
6. [Plugin commands](#id-plugin-commands)
7. [Workspace commands](#id-workspace-commands)
 
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
  container     Manage containers (channel or pools) running on ProconTEL server.
  endpoint      Manage endpoints running on ProconTEL server.
  import        Import PEX file.
  plugin        Manage plugins installed on ProconTEL server.
  workspace     Manage workspaces running on ProconTEL server.

Run 'procontelCLI [command] --help' for more information about a command.
```

<div id='id-container-commands'/>

## 3. Container commands

Create a pool called TestPool in workspace TestWorkspace.
```csharp
.\procontecli.exe container new -p -w TestWorkspace TestPool
```
<br/>

Create a channel called TestChannel in workspace TestWorkspace.
```csharp
.\procontecli.exe container new -w TestWorkspace TestChannel
```
to be continued...
<div id='id-endpoint-commands'/>

## 4. Endpoint commands

Create new endpoint called TestEndpoint in the channel called TestChannel from TestPlugin plugin on localhost
```csharp
.\procontecli.exe endpoint new -c TestChannel -p TestPlugin.Endpoint@TestPlugin -s localhost
```
One remark: this: <b>TestPlugin.Endpoint@TestPlugin</b> hopefully will be replaced by something better in the newer version of ProcontelCLI. It's built as namespace of endpoint class @ name of plugin.

<br/>

Display list of endpoint running on connected ProconTel version.
```csharp
.\procontecli.exe endpoint list -s localhost:9000
```
<br/>

Display parameters of endpoint called TestEndpoint.
```csharp
.\procontecli.exe endpoint params TestEndpoint -s localhost:9000
```
<br/>

Update parameter ActsAsProvider to ```true``` of endpoint called TestEndpoint.
```csharp
.\procontecli.exe endpoint params TestEndpoint -u="ActsAsProvider=true" -s localhost:9000
```
<br/>

Display internal configuration of endpoint called TestEndpoint.
```csharp
.\procontecli.exe endpoint config TestEndpoint -s localhost:9000
```
<br/>

Update internal configuration to ```CONFIGURATION_VALUE``` of endpoint called TestEndpoint.
```csharp
.\procontecli.exe endpoint config TestEndpoint -u="CONFIGURATION_VALUE" -s localhost:9000
```
<br/>

Load internal configuration from local file ```C:\configuration.txt``` of endpoint called TestEndpoint.
```csharp
.\procontecli.exe endpoint config TestEndpoint -f="C:\configuration.txt" -s localhost:9000
```
<br/>

Replace xml internal configuration property of endpoint called TestEndpoint.
```csharp
.\procontecli.exe endpoint config TestEndpoint -r-xml="PluginConfiguration/MethodName=NEW_VALUE" -s localhost:9000
```
<br/>

Replace json internal configuration property of endpoint called TestEndpoint.
```csharp
.\procontecli.exe endpoint config TestEndpoint -r-json="PluginConfiguration.MethodName=NEW_VALUE" -s localhost:9000
```

<div id='id-import-commands'/>

## 5. Import commands
*Chapter in build*

<div id='id-plugin-commands'/>

## 6. Plugin commands
Install plugin called Test Plugin 
```csharp
.\procontecli.exe plugin install D:\SampleProject\TestPlugin.dll
```
<br/>

Install plugin called Test Plugin with dependent an additional dll binaries 
```csharp
.\procontecli.exe plugin install D:\SampleProject\TestPlugin.dll -f D:\SampleProject\contrib\|*.dll||R
```
Where 'R' is a flag to search for defined files recursively in mentioned path.

</br>

Install plugin called Test Plugin with dependent an additional dll binaries from two directories
(additional directories require adding next -f parameter)
```csharp
.\procontecli.exe plugin install D:\SampleProject\TestPlugin.dll -f D:\SampleProject\contrib\|*.dll||R -f D:\SampleProject\additionalLibs\|*.dll||R
```
<br/>

<div id='id-workspace-commands'/>

## 7. Workspace commands
Create new workspace called TestWorkspace
```csharp
.\procontecli.exe workspace new TestWorkspace
```
<br/>

to be continued...