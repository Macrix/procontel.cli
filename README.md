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
*Chapter in build*

<div id='id-endpoint-commands'/>

## 4. Endpoint commands

| Commands | Description  | 
| :---  |:---|
| .\ProconTelCli endpoint list -s localhost:9000 --force-tcp | Display list of endpoint running on connected ProconTel version.  |
| .\ProconTelCLI.exe endpoint params __ENDPOINT_NAME__ -s localhost:9000 --force-tcp |  Display endpoint parameters. |
| .\ProconTelCLI.exe endpoint params __ENDPOINT_NAME__ -u="ActsAsProvider=true" -s localhost:9000 --force-tcp |  Update endpoint parameter ActsAsProvider to ```true```. |
| .\ProconTelCLI.exe endpoint config __ENDPOINT_NAME__ -s localhost:9000 --force-tcp |   Display internal endpoint configuration. |
| .\ProconTelCLI.exe endpoint config __ENDPOINT_NAME__ -u="CONFIGURATION_VALUE" -s localhost:9000 --force-tcp |   Update internal endpoint configuration to ```CONFIGURATION_VALUE```. |
| .\ProconTelCLI.exe endpoint config __ENDPOINT_NAME__ -f="C:\configuration.txt" -s localhost:9000 --force-tcp |   Load internal endpoint configuration from local file ```C:\configuration.txt```. |
| .\ProconTelCLI.exe endpoint config __ENDPOINT_NAME__ -r-xml="PluginConfiguration/MethodName=NEW_VALUE" -s localhost:9000 --force-tcp |   Replace xml internal endpoint configuration property. |
| .\ProconTelCLI.exe endpoint config __ENDPOINT_NAME__ -r-json="PluginConfiguration.MethodName=NEW_VALUE" -s localhost:9000 --force-tcp |   Replace json internal endpoint configuration property. |
<div id='id-import-commands'/>

## 5. Import commands
*Chapter in build*

<div id='id-plugin-commands'/>

## 6. Plugin commands
*Chapter in build*

<div id='id-workspace-commands'/>

## 7. Workspace commands
*Chapter in build*
