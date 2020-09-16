Shared Device Setting REST API Design 
==========================

## PUT /ServicesAPI/API/V1/CMDB/SharedDeviceSettings/APIServerSetting

This API is used to update device API server settings in current domain. The response of this API will return a list in JSON format.<br>

## Detail Information

>**Title:** Update device API server settings API

>**Version:** 05/27/2020

>**API Server URL:** http(s)://IP Address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/SharedDeviceSettings/APIServerSetting

>**Authentication:**

|**Type**|**In**|**Name**|
|------|------|------|
|Bearer Authentication|Headers|Authentication token|

## Request body (*required)

|**Name**|**Type**|**Description**|
|------|------|------|
|shareDeviceSettings.HostName*| string | Device hostname. |
|shareDeviceSettings.ManageIp* | string | Device management IP address. |
|shareDeviceSettings.API_setting| object list | API servers applied to current device. |
|shareDeviceSettings.API_setting.API_plugin| string | name of applied API plugin. |
|shareDeviceSettings.API_setting.API_server| object | applied API server. |
|shareDeviceSettings.API_setting.API_server.name| string | applied API servers name. |

***Note:*** Input body also support Json list with multiple device setting elements for bulk changes. And the ***maximum*** number for bulk changes is ***100***.


```python
### Single Change
API Body = {  
        "HostName" : "CP-SW1",
        "ManageIp" : "192.168.0.58",
        "API_setting" : [
                {
                    "API_plugin" : "string",
                    "API_server" : {
                        "name" : "string"/null
                    }     
                },
                {
                    "API_plugin" : "string",
                    "API_server" : {
                        "name" : "string"/null
                    }  
                },
                {
                    "API_plugin" : "string",
                    "API_server" : {
                        "name" : "string"/null
                    }     
                },
                .
                .
                .
          ]
}

### Bulk Changes with a json list length <= 100
API Body = [
    {  
        "HostName" : "CP-SW1",
        "ManageIp" : "192.168.0.58",
        "API_setting" : [
                {
                    "API_plugin" : "string",
                    "API_server" : {
                        "name" : "string"/null
                    }     
                },
                {
                    "API_plugin" : "string",
                    "API_server" : {
                        "name" : "string"/null
                    }  
                },
                {
                    "API_plugin" : "string",
                    "API_server" : {
                        "name" : "string"/null
                    }     
                },
                .
                .
                .
          ]
    },
    {  
        "HostName" : "CP-SW2",
        "ManageIp" : "192.168.0.59",
        "API_setting" : [
                {
                    "API_plugin" : "string",
                    "API_server" : {
                        "name" : "string"/null
                    }     
                },
                {
                    "API_plugin" : "string",
                    "API_server" : {
                        "name" : "string"/null
                    }  
                },
                {
                    "API_plugin" : "string",
                    "API_server" : {
                        "name" : "string"/null
                    }     
                },
                .
                .
                .
          ]
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
