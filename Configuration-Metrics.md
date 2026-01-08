# AREDN Network Configuration Information and Metrics Data  
  
Version 1.5 - January 8th, 2026  
  
## Goals and Objectives  
  
The New England Mesh network is growing both horizontally (more nodes and additional local mesh networks) and vertically (new and additional types of Services). The administration load of maintaining configuration information for Dashboards, Monitoring Systems, Camera Systems, etc., has become difficult. This is resulting in a significant lag in support for the current network configuration by critical management and services tools.  
  
A system is needed that automatically determines the state of the AREDN network configuration at the New England-wide level and provides the resulting configuration information programmatically. This will enable our management and service toolset to automatically respond to network changes without requiring manual administrative actions.  
##   
### Target Use Cases  
  
Here are some of the planned applications for this system.   
* Automatic discovery of new and reconfigured AREDN nodes and Services  
* Automatic configuration of RF Dashboards  
* Automatic configuration of Network Monitoring tools  
* Generation of up-to-date Release and hardware information to facilitate Upgrade Management  
* Generation of Performance Monitoring  Dashboards (CPU, Memory, Routing Table Size and Churn, LQM, etc.)  
* Semi-automatic configuration of Alarming and Notification systems  
* Automatic generation of Inventory reports  
* Configuration of visualization tools (example, graphical display of network connectivity)  
* Configuration input for use by Agentic AI Applications  
  
These goals will be achieved, in part, using Agentic Artificial Intelligence (AI) applications.  
  
## Format  
  
Configuration files will be JSON formatted.  
  
## Data Schema  
  
Information about the configuration and operation of nodes in the New England Mesh network is stored in three JSON configuration files. The JSON files represent a network composed of segments, node types, and individual nodes.  
  
* The** Segments* (Segments.json)*** define geographical or logical network areas (e.g., MVARA, Cape). Each segment has an ID, a name, valid subsegments, and a description.  
* **Node Types** (***types.json)*** categorize network devices (e.g., RF, SN). Each type has an ID, a name, valid subtypes, and a description.  
* **Nodes** (***nodes.json) ***represent individual devices within the network. Each node is associated with a segment and a type, which together identify its location and device category.  
  
The relationships between these entities define the network’s structure. Nodes belong to segments and are of a specific type. This organization enables a clear, structured representation of the network’s topology and device distribution.  
  
  
### Segment/Sub-Segement/Group Tuplet Records  
  
This table defines the allowed combinations of Segment and Sub-Segment value pairs.  
  

| Segment     | Sub-Segment          | Description               |
| ----------- | -------------------- | ------------------------- |
| MVARA       | N1MVA, NG1P, * (All) | MVARA NH, ME, MA Network  |
| Cape        | Main, Other, * (All) | Cape Cod, MA Network      |
| RI-CT       | Main, Other, * (All) | "RI, CT Network           |
| New England | Core, Other, * (All) | New England Core Services |
| Unknown     | Other                | Unknown Network           |
| All         | All                  | New England AREDN         |
  
** Additional groups will likely be added to further subdivide this segment/subsegment.  
  
###  Type Records  
  
This table defines the allowed Device, Service, and other ***Types***.  
  

| Type | Sub-Type(s) | Description |
| ---- | ---------------------------------------------------------------------------------------------------------------- | ------------------ |
| RF | 900 MHz HaLow Omni, 900 MHz HaLow Station, 5 GHz Pt-Pt, 5 GHz Omni, 5 GHz Sector, Other | AREDN RF Link |
| SN | New England, Other | Supernode Gateway |
| TGW | User, Camera, NE Mesh, DMR & Municipal, Experimental & Intermittent, Other | Tunnel Gateway |
| TUN | End-User, Admin, DMR, Municipal, Expriemental, Intermittent, Portable, Other | User Tunnel Router |
| CAM | PTZ", Fixed, Legacy Fixed, Unsecure, Other | AREDN Camera |
| SVC | RF Performance, Network Status, Power Status, Camera Server, Weather, NTP Server, Information, PBX, eMail, Other | AREDN Service |
| UNKN | Other | Unknown Node Type |
  
  
### Node Records   

| Mesh Segment | Mesh Sub-Segment | Type | Sub-Type | Device Name | Description |
| ------------------------------------------- | ----------------------- | ---------------------- | ---------------------- | ------------------------ | ---------------------------------------------------------- |
| New England, MVARA Mesh, RI Mesh, Cape Mesh | N1MVA, NG1P, Core, etc. | (See Type table above) | (See Type table above) | (See below for examples) | Test Description for Device (use this in Dashboards, etc.) |
  
  
### Node Table Example  
  

| Mesh Segment | Mesh Subsegment | Type | Sub-type | Device Name | Description |
| ------------ | --------------- | ---- | -------------- | ----------------------- | ----------------------- |
| MVARA Mesh | N1MVA | RF | 5 GHz Pt-Pt | N1MVA-Hollis1-NH-MAS | Mason to Hollis RF Link |
| MVARA Mesh | N1MVA | RF | 5 GHz Pt-Pt | N1MVA-Mason1-NH-HLS | Hollis to Mason RF Link |
| New England | Core | TGW | User | AB1OC-Hollis-NH-TGW1 | User Tunnel GW #1 |
| New England | Core | SN | New England | AB1OC-HNH-SUPERNODE | New England Supernode |
| MVARA Mesh | N1MVA | TUN | Admin | AB1OC-Hollis-NH-TUN1 | AB1OC Tunnel Router |
| MVARA Mesh | N1MVA | CAM | Unsecure | W1EAA-Goffstown-NH-CAM1 | W1EAA Turkey CAM |
| New England | Core | SVC | RF Performance | MVARA-dash | N1MVA RF Dashboard |
  
** Additional groups will likely be added to further subdivide this segment/subsegment.  
  
### JSON Example for the Nodes Table (nodes.json)  
  
**{**  
**	“nodes": [**  
**		{**  
**			“id”: 1,**  
**			“segment”: “MVARA Mesh”,**  
**			“subsegment”: “N1MVA”,**  
**			“type”: “RF”,**  
**			"subtype": "5 GHz Pt-Pt",**  
**			“devicename”:  “N1MVA-Chester3-NH-HVL”,**  
**			“description”: “Chester, NH to Haverhill, MA RF Link”**  
**		},**  
**		{**  
**			“id”: 2,**  
**			“segment”: “MVARA Mesh”,**  
**			“subsegment”: “N1MVA”,**  
**			“type”: “RF”,**  
**			"subtype": "5 GHz Pt-Pt",**  
**			“devicename”:  “N1MVA-Gunstock2-NH-FRL”,**  
**			“description”: “Gunstock Mt., NH to Franklin, NH RF Link”**  
**		},**  
**	…**  
**	]**  
**}**  
  
### Other JSON Configuration Files  
  
* **segments.json **- Specifies a list of allowed ***Segment / Subsegment*** pairs. Also includes an ***All*** choice for both levels.  
* **types.json** - Specifies a list of allowed ***Types***. Also includes an ***All*** Choice.  
  
See the Notes on Dashboards section below for details on handling the ***All*** options.  
  
### Combined JSON Configuration File  
  
The three configuration files are combined and validated using AI. The resulting file, ne-mesh.json, contains three objects corresponding to the information in the source JSON files. See the AI subsection in the following section for information on how AI is used to create and validate the combined file. The structure of the combined file (***ne-mesh.json***) is as follows:  
  
{  
	“segments”: [  
		// Array of allowed segment records and allowed subsegment values  
	],  
	“types”: [  
		// Array of allowed node type records and the allowed subtype values  
	],  
	“nodes”: [  
		// Array of records describing the discovered node  
	]  
}  
  
## Accessing JSON Configuration Data  
  
We’ve configured a site that exposes a REST API for querying the JSON configuration. Here are some example queries -  
  
* https://<New England AREDN TSDB>:<port>/segments - Display all records in the Segments Table  
* https://<New England AREDN TSDB>:<port>/nodes?devicename=N1MVA-Uncanoonuc-NH-CRT - Lookup the record in the Nodes Table for N1MVA-Uncanoonuc-NH-CRT.  
* https://<New England AREDN TSDB>:<port>/nodes?description_like=ME - Look up nodes that have the abbreviated state of Maine (ME) in them  
* https://<New England AREDN TSDB>:<port>/nodes?description_like=me&case_insensitive=true - Same as previous query, but case insensitive  
  
More information on query formats is available [here](https://github.com/typicode/json-server). Using an AI LLM to generate the REST API URIs can be a significant timesaver.  We are using Google’s [Gemma3:27b](https://ai.google.dev/gemma/docs/core) LLM for this purpose. You can download and run this LLM using ++[Ollama](https://ollama.com/)++.  
  
Access is encrypted via https/SSL and is governed by an Access Control List (ACL). Please get in touch with [ab1oc@arrl.org](mailto:ab1oc@arrl.org) if you need access.  
   
  
## Data Discovery and Configuration Generation  
  
The configuration files representing the current state of the New England Mesh will be automatically generated or updated daily. This will be done by a daemon that will automatically crawl the local mesh to discover all nodes. A prototype of the daemon has been completed to evaluate feasibility and performance.  
  
There will also be an option to manually trigger the crawl/update process.  
  
### Data Collection and Storage  
  
* Data for all discovered nodes will be accumulated in a Prometheus time-series database.  
* Data sampling intervals will be configurable by device/service ***Type***.  
* Some device and service ***Types*** will likely require custom data adapters to allow Prometheus to collect and store metrics. These will be documented separately as they are created.  
  
### Node Classification, Data Refinement, and Validation Using AI  
  
A locally hosted AI LLM ([gemma3:27b](https://ai.google.dev/gemma/docs/core)) is used to perform the following functions:  
  
* Determine the appropriate ***segment***, ***subsegment***, ***type***, and ***subtype*** for each node discovered during crawling.  
* Combine the resulting ***nodes.json*** file with the corresponding ***segments.json*** and ***types.json*** files to create the*** ne-mesh.json*** file, which is accessible via an external URL and a [JSON REST API](https://restfulapi.net/introduction-to-json/).  
* Validate that the resulting ne-mesh.json contains valid data.  
  
The AI prompts used are included in the Appendix. This area is a work in progress and will evolve as we gain experience with the associated LLM and tools. At some point, we expect to generate an Agentic AI tool that will fully automate the entire crawl and generation process.  
  
### Access to JSON information in Grafana  
  
It appears that the [Grafana Infinity Plugin](https://grafana.com/grafana/plugins/yesoreyeram-infinity-datasource/) is a useful tool for accessing JSON data in Grafana dashboards. We will set up a secure web server to expose a REST API for the ***ne-mesh.json*** file (see the previous section for details)  
  
We need to prototype this scenario. More to follow on accessing the JSON data.  
  
## Accessing Node Data  
  
We have made the production Prometheus Time Series Database (TSDB) accessible in a read-only format. Queries can be made using a web browser or from inside Grafana using the following URL -  
  
- Please contact AB1OC at [ab1oc@arrl.org](mailto:ab1oc@arrl.org) for access information  
  
This URI supports Prometheus [PromQL](https://promlabs.com/promql-cheat-sheet/) queries and can be used as a data source inside Grafana. Access to the TSDB is encrypted via https/signed certificate.  Access is also governed by an Access Control List (ACL). Please get in touch with [ab1oc@arrl.org](mailto:ab1oc@arrl.org) if you need access.  
  
## Notes on Dashboards  
  
The idea is to parameterize our dashboards in the future, so they update automatically as our mesh grows. The same applies to the allowed values for all query parameters (***Segment***, ***Subsegment***, ***Type***, ***Name***, and ***Description***).  
  
1. Dashboards should allow displays based on Segment/Subsegment choices (ex., NH-ME-Mesh / MVARA)  
2. Device type may be specific to certain kinds of dashboards (e.g., RF Dashboard). In this case, the dashboard should query only nodes of types it knows about and display only data from them.  
3. Some future dashboards may display data from multiple node types. In this case, a field should be provided to select an end-user-specified ***Type*** from the available list.  
4. Dashboard dropdowns that select ***Segment***, ***Subsegment***, or ***Type*** should include an ***All*** option that matches all applicable node records.  
5. Some end-user query specifications can return many entries for a given dashboard panel. It’s probably reasonable to set a limit on the number of items graphed and also include a message like (xxx additional nodes matched) or something similar to let the user know that some of the data was not displayed.  
6. The data display should use the ***Description*** field for labeling lines, table items, etc.  
7. The data display should use the ***Subsegment*** and ***Subtype*** fields to construct the labeling string.  
  
  
## Questions to Answer  
  
1. Other options for dashboard qualification, selection, and grouping?  
2. Plan to include a library of routines or to use a Grafana plugin to access the JSON data and apply transactions using the JSON data.  
3. Need to look into how to include ***Local Devices ***in discovery (AB1OC).  
4. The crawling tools also generate node connectivity information. Should we include these in the configuration JSON files?  
  
## Appendix I - AI Notes and Prompts  
  
Current AI Model used for Classification, Validation, and JSON Configuration Generation:  
  
- [Gemma 3 27B](https://ai.google.dev/gemma/docs/core) is Google's powerful, open-weight, multimodal large language model (LLM) featuring 27 billion parameters, capable of understanding both text and images, boasting a massive 128k token context window, strong multilingual support, and advanced reasoning for complex tasks like chatbots and content generation. It's designed for high performance, efficiency, and ease of deployment, including local quantization, making it a strong choice for developers and researchers building next-gen AI applications.   
  
### Prompt to combine the source JSON files into a single JSON (ne-mesh.json):  
  
- I have three JSON files that are related to each other. Please combine these into a single file with 5 objects: a segments object, a subsegments object, a types object, a subtypes object, and a nodes object. Please preserve the subsegment and subtype values in the node records. Here are the files - <upload the three source JSON files>  
  
### Prompt to validate the information in the resulting combined JSON file:  
  
- Please confirm that all segment, subsegment, type, and subtype pairs in each node record are 1) valid and 2) are valid combinations as defined in the segment and type objects. Here is the rule to validate combinations. A node's subtype is only valid if it is explicitly listed as a subtype in the corresponding type object record that the node record references. A node’s subsegments are only valid if they are expressly listed as a subsegment in the corresponding segments object that the node record references. Please validate the node records using these rules.  
  
### Prompt to determine Segment, Subsegment, Type, and Subtype for each Node   
- TBD at this time. The approach will use the following information to enable the LLM to determine the node type and subtype.  
    * The Prometheus data from the target node (includes information about node type and RF interfaces as well as GPS coordinates  
    * The path (via traceroute) used to locate the node. Access to the various nodes in the NE mesh is structured via a series of Core Gateways. This information helps determine a node's segment and subsegment.  
  
