# Audience #

.NET developers wanting to get a head-start in developing SOAP WMLS Client applications for the WITSML standard.

This document details how to build a simple application using automated tools to parse XML Data Schemas and Server WSDLs, to quickly write the Web and Data interfaces.

The example builds a simple WITSML Client that lists all wells in the store.

The data returned from the stored is deserialized to a C# class, providing access to the data in a native C# Data structure.

# Prerequisites #

  * Microsoft Visual C# 2010 Express or better
  * WITSML 1.3.1.1 Data Schema http://w3.energistics.org/schema/WITSML_Data_Schema_v1311.zip
  * Account in a WITSML Server, or access to the WSDL file. A [Sample WSDL file is provided](SampleWSDL.md)

# Setting up the development environment #

  * Start a new Visual C# 2010 project

  * Select the project type as a Windows Forms Application, set the project name to **WITSML Client from Scratch**

  * Add a reference for **System.Web.Services** in Project ? Add Reference... ? .NET Tab ? System.Web.Services

  * Add the code references for the Serialization and StringReader functions:
```
using System.IO; // for StringReader
using System.Xml.Serialization; // for Serialization 
```

  * Create a user interface in the main for with the following elements:
| **tURL** | Textbox for the WITSML Store URL |
|:---------|:---------------------------------|
| **tUsername** | Textbox for the Username in the WITSML store |
| **tPassword** | Textbox for the Password in the WITSML store |
| **bListWells** | Button |
| **bAdd** | Button |
| **bGet** | Button |
| **bUpdate** | Button |
| **bDelete** | Button |
| **tQuery** | Read-only textbox used to display the query sent to the server |
| **tResponse** | Read-only textbox used to display the response data received from the server |
| **tStatusCode** | Read-only textbox used to display the Status Code returned by the server |
| **tStatusMessage** | Read-only textbox used to display the Status Message returned by the server |
| **tProcessedResponse** | Text Area to display data extracted from the serialized objects |

# WITSML WMLS Client Interface #
## Building the WMLS Client interface ##
  * Use the .NET WSDL.exe program to parse the WITSML Server WSDL file, and generate the C# Class file with necessary methods to access the server. If you have access to a WITSML server, use:

```
wsdl.exe http://server_name/Path/To/WSDL /username:YOUR_USERNAME /password:YOUR_PASSWORD /namespace:WITSML.WSDL /fields /language:CS
```

  * If you only have access to a WSDL file, use instead:

```
wsdl.exe WITSML.wsdl /namespace:WITSML.WSDL /fields /language:CS
```
Where:
| http://server_name/Path/To/WSDL | Published WSDL in the WITSML Store |
|:--------------------------------|:-----------------------------------|
| WITSML.wsdl | Local copy of the WSDL file |
| /username:YOUR\_USERNAME | Username in the WITSML Store |
| /password:YOUR\_PASSWORD | Password in the WITSML Store |
| /language:CS | Output Language (C Sharp) |
| /fields | Output fields instead of properties |

  * Add the output file “WMLS.cs” to the current project, using the Solution Explorer

## Customizing the WITSML Client Interface ##
### Add support for generic URLs ###
The automatically generated WMLS function will be hardcoded to the Server used when building the class using WSDL.exe. I.e:
```
        public WMLS() {
            this.Url = "https://server_name/path/to/wmls.asmx";
        }
```

In order to support other WITSML Servers, change the function to accept arbitrary URLs
```
 public WMLS(string sURL)
 {
         this.Url = sURL;
 }
```

**The property Url is defined in Systems.Web.Services**


### Add support for user credentials ###
The automatically generated WMLS function does not provide authentication interfaces, which is a must for most WITSML Servers. Edit the file WMLS.cs, and change the definition for the function WMLS to:
```
    /// <remarks/>
    public WMLS(string sURL, string sUsername, string sPassword) {
        this.Url = sURL;
        this.Credentials = new System.Net.NetworkCredential (sUsername, sPassword);
    }
```

**The property Credentials is defined in Systems.Web.Services**

# Serializable Classes #
## Building the Serializable Classes ##
  * Download the WITSML 1.3.1.1 Data schema
  * Unzip the ZIP file WITSML\_Data\_Schema\_v1311.zip containing the full WITSML 1.3.1.1 Data Schema to a local folder. In this document we will use the folder name “WITSML\_Data\_Schema\_v1311”
  * Create an output directory “WITSML”. The folder structure is:
```
    Current Directory
    |- WITSML
    |- WITSML_Data_Schema_v1311
```
  * Use one of the following two methods to build the WITSML/WITSML\_1311.cs Class library
  * Create a XSD parameters file XSD\_Class\_Serialization\_Parameters.xml
```
<?xml version="1.0" encoding="utf-8" ?>
<xsd xmlns="http://microsoft.com/dotnet/tools/xsd/" output="WITSML">
	<generateClasses   language="CS"  namespace="WITSML.Client_1311" options="enableDataBinding">
		<schema>WITSML_Data_Schema_v1311\obj_bhaRun.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_cementJob.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_convCore.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_dtsInstalledSystem.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_dtsMeasurement.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_fluidsReport.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_formationMarker.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_log.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_message.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_mudLog.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_opsReport.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_realtime.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_rig.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_risk.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_sidewallCore.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_surveyProgram.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_target.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_trajectory.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_trajectoryStation.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_tubular.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_wbGeometry.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_well.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_wellbore.xsd</schema>
		<schema>WITSML_Data_Schema_v1311\obj_wellLog.xsd</schema>
	</generateClasses >
</xsd>
```

  * Run the XSD command
```
xsd /p:XSD_Class_Serialization_Parameters.xml
```

  * The output filename will be the name of the last xsd file. The following command renames it
```
move tmp\obj_wellLog.cs WITSML_Client_1311.cs
```

  * Remove the temporary directory
```
rmdir tmp
```

  * Add the output file “WITSML\_Client\_1311.cs” to the current project, using the Solution Explorer.

# WITSML Templates #

WITSML queries are template based. The following templates are suggested for all objects:

  * List: Lists the basic ID information for all objects in the container
  * Get: List all details for one object
  * Update: Updates details of one object
  * Delete: Deletes one object

## Sample queries ##

### List Wells: list\_wells.xml ###
```
<wells>
  <well uid="">
    <name/>
  </well>
</wells>
```

### Get Well Detail: get\_well.xml ###
```
<wells xmlns="http://www.witsml.org/schemas/131" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" version="1.3.1.1">
   <well uid="%uid%">
      <name></name>
      <nameLegal />
      <numLicense />
      <numGovt />
      <dTimLicense />
      <field />
      <country />
...
   </well>
</wells>
```

### Update Well: update\_well.xml (The example is limited to updating the well name) ###
```
<wells xmlns="http://www.witsml.org/schemas/131" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" version="1.3.1.1">
  <well uid="%uid%">
    <name>%name%</name>
  </well>
</wells>
```

### Delete Well: delete\_well.xml ###
```
<wells>
  <well uid="%uid%">
    <name/>
  </well>
</wells>
```

# Getting Data from the WITSML Server #

The following code retrieves the list of wells in XML format from the store, using the list\_wells.xml template file.

```
// Set the Object type
string sSobjectType = "well";

// Read the query string
string sQuery = System.IO.File.ReadAllText("list_wells.xml");

// Set OptionsIn
string sOptionsIn = "";

// Create a WITSML Store Client interface object
WMLS W = new WMLS( sURL, sUsername, sPassword );

// Strings returned by the store
string sXML = "";
string sMessage = "";

// Try getting the XML from the store
short iStatus = -1;

iStatus = W.WMLS_GetFromStore( sObjectType, sQuery, sOptionsIn, "", out sXML, out sMessage );

```

The list of common operations provided in WMLS.cs are:

  * GetCap
  * GetFromStore
  * UpdateInStore
  * DeleteFromStore
  * AddToStore

If you would like additional information for the implementation of WITSML Clients, feel free to contact us at cswitsml@roderickc.com