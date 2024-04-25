This repository hosts documentation, sample applications and guidelines for implementing DataPorts. DataPorts facilitate the exchange of data between two parties.

# Getting started
The best way to use DataPorts is to integrate the Azlon.DataPort.Client package into your own software.

Alternatively one of the sample applications can be downloaded and files can be sent/received immediately.

## Azlon.DataPort.Client package
The Azlon.DataPort.Client package is available for .Net and for Java and can be integrated into your own software.

The .Net package can be downloaded from [here](https://github.com/orgs/Azlon-io/packages/nuget/package/Azlon.DataPort.Client) or [here](https://github.com/Azlon-io/DataPorts/tree/master/Development%20Toolkit%20DotNet%20(NuGet%20package))

The java package can be download from [here](https://github.com/Azlon-io/DataPorts/tree/master/Development%20Toolkit%20Java%20(Maven)/DataPortClient%20JAR)

A sample application and more information on how to integrate the package can be found [here](https://github.com/Azlon-io/dataport-cli) (.Net only)

## Sample applications
Two different sample applications are available:

### 1) A desktop tool
- [For Windows](https://github.com/Azlon-io/DataPorts/tree/master/Demo%20Desktop%20Application%20Windows). This tool integrates the .Net package.
- [For OSX](https://github.com/Azlon-io/DataPorts/tree/master/Demo%20Desktop%20Application%20OSX). This tool integrates the Java package.
- [For Linux](https://github.com/Azlon-io/DataPorts/tree/master/Demo%20Desktop%20Application%20Linux%20x64). This tool integrates the Java package.

The desktop tool supports sending and receiving files to/from a DataPort.


### 2) Command line tool
More information on the CLI tool can be found [here](https://github.com/Azlon-io/dataport-cli)

The CLI tool supports receiving files from a DataPort.

## Prerequisites
A DeviceId and SharedAccessKey are provided by your contact person.

## Configuration
The following configuration must be set in the configuration file of the application:
- autoSaveLocation: Path where received files are stored
- Environment: Test|Live
- Name: Name of the DataPort
- DeviceId: Unique DataPort identifier, supplied by your contact person
- SharedAccessKey: Access key for the DataPort, supplied by your contact person
```
<appSettings>
	<add key="autoSaveLocation" value="C:\Dataport_Downloads\" />
</appSettings>
<Dataport>
	<add key="Environment" value="Test" />
	<add key="Name" value="Test DataPort" />
	<add key="DeviceId" value="???" />
	<add key="SharedAccessKey" value="???" />
</Dataport>
```
