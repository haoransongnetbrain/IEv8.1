Shared Device Setting REST API Design 
==========================

## PUT /ServicesAPI/API/V1/CMDB/SharedDeviceSettings/SNMPSetting

This API is used to update device SNMP settings in current domain. The response of this API will return a list in JSON format.<br>

## Detail Information

>**Title:** Update device SNMP settings API

>**Version:** 05/27/2020

>**API Server URL:** http(s)://IP Address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/SharedDeviceSettings/SNMPSetting

>**Authentication:**

|**Type**|**In**|**Name**|
|------|------|------|
|Bearer Authentication|Headers|Authentication token|

## Request body (*required)

|**Name**|**Type**|**Description**|
|------|------|------|
|shareDeviceSettings.HostName| string | Device hostname. |
|shareDeviceSettings.ManageIp | string | Device management IP address. |
|shareDeviceSettings.SNMP_setting| object | SNMP setting of current device. |
|shareDeviceSettings.SNMP_setting.roString| string  | value of device snmp RO.  |
|shareDeviceSettings.SNMP_setting.rwString| string | value of device snmp RWq. |
|shareDeviceSettings.SNMP_setting.snmpPort| integer | SNMP port number. |
|shareDeviceSettings.SNMP_setting.snmpVersion| integer | version number of snmp version for current device |
|shareDeviceSettings.SNMP_setting.UseCustomizedManagementIp| bool | whether current device using the customized management IP.|
|shareDeviceSettings.SNMP_setting.v3| string | Alies name. |
|shareDeviceSettings.SNMP_setting.retrieve_CPU_OID| string | value of customized management IP retrieve CPU OID. |
|shareDeviceSettings.SNMP_setting.retrieve_memory_OID| string | value of customized management IP retrieve memory OID.|
|shareDeviceSettings.SNMP_setting.CustomizedManagementIp| object | SNMP customized management IP setting . |
|shareDeviceSettings.SNMP_setting.CustomizedManagementIp.ManageIp| string | value of customized management IP. |
|shareDeviceSettings.SNMP_setting.CustomizedManagementIp.snmpVersion| string | customized SNMP version. |
|shareDeviceSettings.SNMP_setting.CustomizedManagementIp.LiveStatus| integer | SNMP setting of current device. |
|shareDeviceSettings.SNMP_setting.CustomizedManagementIp.ro| string | value of customized management IP RO. |
|shareDeviceSettings.SNMP_setting.CustomizedManagementIp.rw| string | value of customized management IP RW. |

***Note:*** Input body also support Json list with multiple device setting elements for bulk changes. And the ***maximum*** number for bulk changes is ***100***.

***Example***


```python
### Single Change
API Body = {  
        "HostName" : "CP-SW1",
        "ManageIp" : "192.168.0.58",
        "SNMP_setting" : {
          "roString": "=",
          "rwString": "=",
          "snmpVersion": 1/2/3,
          "snmpPort": 161,
          "v3": "AliesName",
          "UseCustomizedManagementIp": false,
          "retrieve_CPU":"string",
          "retrieve_memory":"string",
          "CustomizedManagementIp": {            
            "ManageIp": "",
            "LiveStatus": int,
            "snmpVersion": "string",
            "ro": "string",
            "rw": "string",
            "v3": "AliesName"
          }  
        }
}

### Bulk Changes with a json list length <= 100
API Body = [
  {  
        "HostName" : "CP-SW1",
        "ManageIp" : "192.168.0.58",
        "SNMP_setting" : {
          "roString": "=",
          "rwString": "=",
          "snmpVersion": 1/2/3,
          "snmpPort": 161,
          "v3": "AliesName",
          "UseCustomizedManagementIp": false,
          "retrieve_CPU":"string",
          "retrieve_memory":"string",
          "CustomizedManagementIp": {            
            "ManageIp": "",
            "LiveStatus": int,
            "snmpVersion": "string",
            "ro": "string",
            "rw": "string",
            "v3": "AliesName"
          }  
        }
  },
  {  
        "HostName" : "CP-SW1",
        "ManageIp" : "192.168.0.58",
        "SNMP_setting" : {
          "roString": "=",
          "rwString": "=",
          "snmpVersion": 1/2/3,
          "snmpPort": 161,
          "v3": "AliesName",
          "UseCustomizedManagementIp": false,
          "retrieve_CPU":"string",
          "retrieve_memory":"string",
          "CustomizedManagementIp": {            
            "ManageIp": "",
            "LiveStatus": int,
            "snmpVersion": "string",
            "ro": "string",
            "rw": "string",
            "v3": "AliesName"
          }  
        }
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
