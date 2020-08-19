
This project contains documentation for the DataPorts project. 
Here the different client versions can be found as well as an example project and the documentation on how to use the DataPort-Client.


## Contents
1. [Project Roadmap](#project-roadmap)
1. [Getting started](#getting-started)
	1. [Prerequisites](#prerequisites)
2. [Request a DataPort address](#request-a-dataport-address)
1. [NuGet Package](#nuget-package)
	1. [Open visual studio](#open-visual-studio)
	1. [Implement Client methods](#implement-client-methods)
	1. [DataPortQuery](#dataportquery)
1. [Example application](#example-application)
	1. [Sending data queries](#sending-data-queries)
1. [Versioning](#versioning)


## Project Roadmap
At the moment the next items are on the roadmap and are being developed:

-	Maven client (Java)
-	.Net Client (C#) 
-	Portal where you can manage your dataport(s)


## Getting started
There are multiple ways to start using DataPorts.
The easiest way is downloading the Example application here.
The alternative way is implementing the NuGet package into your own software application ([Link](#nuget-package)).

### Prerequisites
At this moment the Example application and the NuGet Package are written using C# which is .Net Framework based.
So one of the requirements is a Windows environment with the .Net Framework installed (mostly installed by default).


##Request a DataPort address
Credentials for using DataPorts can be obtained by filling in this form -> [**link**](https://forms.gle/gCzUSkhMFaisPvkBA )


## NuGet Package
Start a new .Net development project in Visual Studio, or embed the client in your existing software.



The next items are required to be able to use the NuGet Package.

- Visual Studio 2017 or later
- The DataPort GitHub repository is cloned to your local disk
- An internet connection

#### Open visual studio ####

1. The First step is to add a (NuGet) Package Source.
1. This can be done by opening the next path in Visual Studio: Tools > NuGet Package Manager > Package Manager Settings. Select "NuGet Package Manager" > "Package Sources" in the tree on the left side.
1. Add a new package source. Point this to the path where the DataPort .Net Client folder is located. Press update and OK.
1. Now you are ready to Add the NuGet Package to your development project


#### Implement Client methods ####

The next methods should be implemented:

1.	Constructor to initialize the Client // Client() or Client(string deviceId, string sharedAccesKey)
1.	Event to receive messages: OnMessageReceived()
1.	Call method to start receiving: StartReceiving()
1.	Call method to stop receiving: StopReceiving()




'

	using Azlon.Dataport.Client;
	using Azlon.Dataport.Model;
	using System;
	using System.Configuration;
	using System.Net;
	
	namespace Dataport
	{
	    public class Form1 : Form
	    {
	        Client dataportClient = new Client();
	
	        public Form1 : Form()
	        {
	            dataportClient = new Client(ConfigurationManager.AppSettings["deviceId"], ConfigurationManager.AppSettings["sharedAccesKey"]);
	            dataportClient.OnMessageReceived += DataportClient_OnMessageReceived;
	            dataportClient.StartReceivingMessages();
	        }
	
	        private void DataportClient_OnMessageReceived(object source, DataPortMessage message)
	        {
	            if (message != null)
	            {
	                DownloadAndSaveMessage(message);
	            }
	        }
	
	        private void DownloadAndSaveMessage(DataPortMessage message)
	        {
	            WebClient wc = new WebClient();
	
	            try
	            {
	                wc.DownloadFile(new Uri(message.DataFile), $"{folder}{message.OriginalFileName}");

					//Process your downloaded message here.
	            }
	            catch (Exception ex)
	            { }
	        }
	    }
	} 
	
	
### DataPortQuery
The DataPort Client supports a way to ask questions to other dataports.
To archieve this, a method on the DataPort Client can be called.
The method is call SendDatportQuery and one of the parameters is the SearchIdentifier. The SearchIdentifier is an enumeration of field on which you can search.

	dataportClient.SendDataportQuery(SearchIdentifiers.GTIN, "8713600053445", destinationDataPort);

The enumeration is included in the DataPort Client package, so this can be expanded at future versions.
At this moment the next options are present for the SearchIdentifier:

- GTIN
- GBIN
- NAME

The result of the DataPortQuery is fully dependant of the DataPort-implementation of the receiving party. 



## Example application
Download the ZIP from this repository and extract it into a folder on your computer.
Locate the Dataport.exe.config file and open this with a texteditor (Notepad or Notepad++).
Find the next lines in the file and fill in a value for dataportName, deviceId and sharedAccesKey.

	<add key="dataportName" value="Replace_This" />
    <add key="deviceId" value="Replace_This" /> 
    <add key="sharedAccesKey" value="Replace_This" />

After this you can start the tool and start sending files to other dataports.

### Sending data queries
With the example application it is also possible to send dataqueries to other DataPorts.
A dataquery contains a key field and a value for this key field. For example: you can search on keyfield 'GTIN' and value '8713600053445'. When you send this query to a DataPort, the DataPort will receive this query and will be able to send and answer back to asking DataPort.

**Note:** it's depending on the receiving DataPort if you will get an answer. The receiving DataPort must implement a search method for this to work. This is not mandatory for using DataPorts.

### Prerequisites
- Windows computer with .Net Framework installed (mostly installed by default)
- deviceId and sharedAccesKey supplied by Azlon



## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/FcAalst/DataPorts/tags).
