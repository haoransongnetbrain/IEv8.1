Shared Device Setting REST API Design 
==========================

## PUT /ServicesAPI/API/V2/CMDB/SharedDeviceSettings/BasicSetting

This API is used to update device basic settings in current domain. The response of this API will return a list in JSON format.<br>

**Note:** the privilege requirement is following UI setting: except Guest role, all other roles can access these three PUT APIs.

## Detail Information

>**Title:** Update device basic settings API

>**Version:** 06/18/2020

>**API Server URL:** http(s)://IP Address of NetBrain Web API Server/ServicesAPI/API/V2/CMDB/SharedDeviceSettings/BasicSetting

>**Authentication:**

|**Type**|**In**|**Name**|
|------|------|------|
|Bearer Authentication|Headers|Authentication token|

## Request body (*required)

|**Name**|**Type**|**Description**|
|------|------|------|
|shareDeviceSettings.HostName*| string | Device hostname. |
|shareDeviceSettings.ManageIp* | string | Device management IP address. |
|shareDeviceSettings.Locked| bool | Whether the device setting has been locked. |
|shareDeviceSettings.LiveStatus| integer | live status of current device. |

***Note:*** Input body also support Json list with multiple device setting elements for bulk changes. And the ***maximum*** number for bulk changes is ***100***.

***Example***


```python
### Single Change
API Body = {  
        "Locked" : False,
        "LiveStatus" : 1,
        "HostName" : "CP-SW1",
        "ManageIp" : "192.168.0.58"
}

### Bulk Changes with a json list length <= 100
API Body = [
        {  
                "Locked" : False,
                "LiveStatus" : 1,
                "HostName" : "CP-SW1",
                "ManageIp" : "192.168.0.58"
        },
        {  
                "Locked" : False,
                "LiveStatus" : 1,
                "HostName" : "CP-SW2",
                "ManageIp" : "192.168.0.59"
        },
        {  
                "Locked" : False,
                "LiveStatus" : 1,
                "HostName" : "CP-SW3",
                "ManageIp" : "192.168.0.60"
        },
        .
        .
        .
]
```

## Headers

>**Data Format Headers**

|**Name**|**Type**|**Description**|
|------|------|------|
|Content-Type|string|support "application/json"|  
|Accept|string|support "application/json"|

>**Authorization Headers**

|**Name**|**Type**|**Description**|
|------|------|------|
|token|string|Authentication token, get from login API.|

## Response


|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|statusCode| integer | The returned status code of executing the API. |
|statusDescription| string | The explanation of the status code. |
| ### | ### |<br>**790200** -- Succeed <br> **794011** -- OperationFailed: There is no match hostname or managementip founded.<br>This device is locked, can not be updated.<br>Invalid Manage IP. <br> **793001** -- InternalServerError: System framework level error|
|failedDevices| list | All update failed devices during current HTTP request. |
|failedDevices.hostname| string | Update failed device hostname. |
|failedDevices.error_msg| string | Reason for update failed device. |
