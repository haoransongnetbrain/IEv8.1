
# Device API Design

## ***POST*** /V1/ChangeAnalysis/ExportReport
Calling this API to export the change analysis.

***Note:*** To enable this API in V8.02 environment, a patch is needed, please contact with NetBrain team to apply the patch.

## Detail Information

> **Title** : Export the change analysis report API<br>

> **Version** : 10/22/2020.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/ChangeAnalysis/ExportReport

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Headers

> **Data Format Headers**

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| Content-Type | string  | support "application/json" |
| Accept | string  | support "application/json" |

> **Authorization Headers**

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| token | string  | Authentication token, get from login API. |

## Query Parameters(****required***)

>No request query parameter.

## Request body(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|StartDate*|String|Define the start date of the report in ISO8601 format|
|EndDate*|String|Define the end date of the report in ISO8601 format|
|DataTypeList|List of object|The monitored data type to be included in the report. By default, it is the config files unless specified|
|DataTypeList.DataType|String|See table below for data type code details.|
|DeviceIDList|List of object|The monitored devices to be included in the report. By default, the scope is all devices in the current domain unless specified.|
|DeviceIDList.ID|String|Device ID |

#### Supported dataType 
|**DataTypeList.DataType**|**DataType**|**DataTypeList.DataType**|**DataType**|
|------|------|------|------|
|config/config|Configuration Files|nctTable/IPsec VPN Table[Real-time]|IPSec VPN Table [Real-time]|
|sysTable/routeTable|Route Table |nctTable/IPv6 Route Table|IPv6 Route Table|
|sysTable/arpTable|ARP Table|nctTable/L2VPN Forwarding Table[Real-time]|L2VPN Forwarding Table[Real-time]|
|sysTable/macTable|MAC Table|nctTable/LDP Table|LDP Table|
|sysTable/cdpTable|NDP Table|nctTable/Ltm Pool Table|Ltm Pool Table|
|sysTable/stpTable|STP Table|nctTable/LWAP Summary Table|LWAP Summary Table|
|sysTable/bgpNbrTable|BGP Advertised-route table|nctTable/Management ARP Table|Management ARP Table|
|nctTable/ARP Switch Table|ARP Switch Table|nctTable/Management Route Table|Management Route Table|
|nctTable/ARP Table[Mac Learning Type]|ARP Table [Mac Learning Type]|nctTable/MPLS Aggregated Label|MPLS Aggregated Label|
|nctTable/BFD Table|BFD Table|nctTable/MPLS LFIB|MPLS LFIB|
|11|BGP All VPNv4 Advertised Route Table|nctTable/MPLS TE|MPLS TE|
|nctTable/BGP Neighbors|BGP Neighbors|nctTable/MPLS VPNv4 Label|MPLS VPNv4 Label|
|nctTable/BGP Network Table|BGP Network Table|nctTable/Multicast Route Table|Multicast Route Table|
|nctTable/BGP Received Route Table|BGP Received Route Table|nctTable/NAT Table|NAT Table|
|nctTable/BGP VPNv4 Imported Routes|BGP VPNv4 Imported Routes|nctTable/NAT Table[Real-time]|NAT Tabel[Real-time]|
|nctTable/Bridging Group|Bridging Group|nctTable/ NHRP Table|NHRP Table|
|nctTable/Client Summary Table|Client Summary Table|nctTable/ NHTP Table|NHTP Table|
|nctTable/Contract Table|Contract Table|nctTable/OSPF Neighbors|OSPF Neighbors |
|nctTable/COOP Endpoint Table|COOP Endpoint Table|nctTable/OTV Table[Real-time]|OTV Table[Real-time]|
|nctTable/EPG Contract Table|EPG Contract Table|nctTable/Policy Content|Policy Content|
|nctTable/External EPG Mapping Table|External EPG Mapping Table|nctTable/Policy Table|Policy Table|
|nctTable/Fabric ISL|Fabric ISL|nctTable/QoS Mapping Table|QoS Mapping Table|
|nctTable/Fabric Route Topology|Fabric Route Topology |nctTable/Segment Routing SRGB|Segment Routing SRGB|
|nctTable/Fabric Trunk|Fabric Trunk|nctTable/Service Graph Mapping Table|Service Graph Mapping Table|
|nctTable/FabricPath Route Table|Fabric Path Route Table|nctTable/SPB MAC Table|SPB MAC Table|
|nctTable/Filter Table|Filter Table|nctTable/Uplink Table|Uplink Table|
|nctTable/ FabricPath Route Table|FabricPath Route Table|nctTable/Virtual Server Table|Virtual Server Table|
|nctTable/Filter Table|Filter Table|nctTable/Virtual Wire|Virtual Wire|
|nctTable/FlexConnect Summary Table|FlexConnect Summary Table|nctTable/VM Mapping Table|VM Mapping Table|
|nctTable/Fortigate Route Table|Fortigate Route Table|nctTable/VXLAN Address Table|VXLAN Address Table|
|nctTable/Global Endpoint Table|Global Endpoint Table|nctTable/VXLAN Peer Table|VXLAN Peer Table|
|nctTable/GRE Tunnels|GRE Tunnels|nctTable/Wireless Endpoint Table|Wireless Endpoint Table|
|nctTable/HA State|HA State|nctTable/WLAN Summary Table|WLAN Summary Table|
|nctTable/Host Guest Table|Host Guest Table|nctTable/Zone Table|Zone Table|
|nctTable/IPsec VPN Table|IPSec VPN Table|nctTable/Zoning Rule Priority Table|Zoning Rule Priority Table|
|nctTable/Zoning Rule Table|Zoning Rule Table| ### | ### |

> ***Example***


```python
API Body = {
    "StartDate" : "2020-06-01T04:00:00.000Z",
    "EndDate" : "2020-06-02T04:00:00.000Z",
    "DataTypeList": ["config/config", ... ],
    "DeviceIDList": []
}

```

## Response

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|statusCode| integer | The returned status code of executing the API.  |
|statusDescription| string | The explanation of the status code.  |
|statusDescription.OK| string | Succeed  |
|statusDescription.OperationFailed| string | Failed.  |
|statusDescription.ParameterNULL| string | The required parameters in request body cannot be empty.  |
|statusDescription.Data Not Enabled| string | Change analysis is not enabled or requested data type is not enabled in change analysis setting.  |
|statusDescription.No Access to device| string | User does not have privilege to access the requested devices.  |
|statusDescription.Internal Server Error| string | System Failure.  |



```python

```
