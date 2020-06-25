

# BasicSetting

## PUT /ServicesAPI/API/V1/CMDB/SharedDeviceSettings/BasicSetting

This API is used to update device basic settings in current domain. The response of this API will return a list in JSON format.<br>

**Note:** the privilege requirement is following UI setting: except Guest role, all other roles can access these three PUT APIs.

## Detail Information

>**Title:** Update device basic settings API

>**Version:** 06/18/2020

>**API Server URL:** http(s)://IP Address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/SharedDeviceSettings/BasicSetting

>**Authentication:**

|**Type**|**In**|**Name**|
|------|------|------|
|Bearer Authentication|Headers|Authentication token|

## Request body (*required)

|**Name**|**Type**|**Description**|
|------|------|------|
|shareDeviceSettings.LiveHostName*| string | Device hostname. |
|shareDeviceSettings.ManageIp* | string | Device management IP address. |
|shareDeviceSettings.ApplianceId | string | Name of front server. |
|shareDeviceSettings.Locked| bool | Whether the device setting has been locked. |
|shareDeviceSettings.LiveStatus| integer | live status of current device. |

***Example***


```python
API Body = {  
        "Locked" : False,
        "LiveStatus" : 1,
        "LiveHostName" : "CP-SW1",
        "ApplianceId" : "FS1",
        "ManageIp" : "192.168.0.58
}
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
|statusCode|integer|Code issued by NetBrain server indicating the execution result.|
|statusDescription|string|The explanation of the status code.|


```python
# success
{
    "statusCode": 790200,
    "statusDescription": "Device <Hostname> <CLI attributes> have been updated successfully."
}

# failed
# wrong device hostname or IP
{
    "statusCode": 790XXX,
    "statusDescription": "Device <Hostname> dosen't exsit in current domain."
}
# no privilege
{
    "statusCode": 790XXX,
    "statusDescription": "Your don't have enough privilege to change <Hostname> CLI settings."
}
# attributes not support to be changed
{
    "statusCode": 790XXX,
    "statusDescription": "<CLI attributes> cannot be changed by API call."
}
```


# CLISetting

## PUT /ServicesAPI/API/V1/CMDB/SharedDeviceSettings/CLISetting

This API is used to update device CLI settings in current domain. The response of this API will return a list in JSON format.<br>

**Note:** the privilege requirement is following UI setting: except Guest role, all other roles can access these three PUT APIs.

## Detail Information

>**Title:** Update device CLI settings API

>**Version:** 05/27/2020

>**API Server URL:** http(s)://IP Address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/SharedDeviceSettings/CLISetting

>**Authentication:**

|**Type**|**In**|**Name**|
|------|------|------|
|Bearer Authentication|Headers|Authentication token|

## Request body (*required)

|**Name**|**Type**|**Description**|
|------|------|------|
|shareDeviceSettings.LiveHostName*| string | Device hostname. |
|shareDeviceSettings.ManageIp* | string | Device management IP address. |
|shareDeviceSettings.CLI_setting| object | CLI setting of current device. |
|shareDeviceSettings.CLI_setting.mode| string | mode for cli access. |
|shareDeviceSettings.CLI_setting.access_mode| string | access mode. |
|shareDeviceSettings.CLI_setting.access_mode_port| integer | port number of access mode. |
|shareDeviceSettings.CLI_setting.CLI_credential_username| string | usename for CLI credential. |
|shareDeviceSettings.CLI_setting.CLI_credential_password| string | password for CLI credential. |
|shareDeviceSettings.CLI_setting.privilege_username| string | device privilege username. |
|shareDeviceSettings.CLI_setting.privilege_password| string | device privilege password. |
|shareDeviceSettings.CLI_setting.Telnet_Proxy_Id| string | Telnet_Proxy_Id. |
|shareDeviceSettings.CLI_setting.Telnet_Proxy_Id_For_Smart_CLI| string | Telnet_Proxy_Id_For_Smart_CLI. |
|shareDeviceSettings.CLI_setting.prompt_settings| object | object for CLI prompt settings. |
|shareDeviceSettings.CLI_setting.prompt_settings.non_privilege_prompt| string | non_privilege_prompt. |
|shareDeviceSettings.CLI_setting.prompt_settings.privilege_prompt| string | privilege_prompt. |
|shareDeviceSettings.CLI_setting.prompt_settings.login_prompt_username| string | login_prompt_username. |
|shareDeviceSettings.CLI_setting.prompt_settings.login_prompt_password| string | login_prompt_password. |
|shareDeviceSettings.CLI_setting.prompt_settings.privilege_login_prompt| string | privilege_login_prompt_username. |
|shareDeviceSettings.CLI_setting.prompt_settings.privilege_password_prompt| string | privilege_password_prompt. |
|shareDeviceSettings.CLI_setting.advenced_setting| object | object for CLI advanced settings. |
|shareDeviceSettings.CLI_setting.advenced_setting.ForceTimeout| integer | force time out for CLI access |
|shareDeviceSettings.CLI_setting.advenced_setting.SSH_key_setting| object | object for CLI SSH finger print settings. |
|shareDeviceSettings.CLI_setting.advenced_setting.SSH_key_setting.checkSSHFingerprint| bool | enable or not for SSH Fingerprint key. |
|shareDeviceSettings.CLI_setting.advenced_setting.SSH_key_setting.SSHFingerprintKey| string | SSH fingerprint key value. |

***Example***


```python
API Body = { 
        "LiveHostName" : "CP-SW1",
        "ManageIp" : "192.168.0.58",
        "CLI_setting" : {
            "mode":"string",
            "access_mode":"string",
            "access_mode_port":"string"/int,
            "CLI_credential_username":"string",
            "CLI_credential_Password":"string",
            "privilege_username":"string",
            "privilege_password":"string",           
            "Telnet_Proxy_Id" : "string",
            "Telnet_Proxy_Id_For_Smart_CLI" : "string"，
            "prompt_settings":{
                "non_privilege_prompt":"string",
                "privilege_prompt":"string",
                "login_prompt_username":"string",
                "login_prompt_password":"string",
                "privilege_login_prompt":"string"
                "privilege_password_prompt":"string"
            },
            "advenced_setting":{
                "ForceTimeout" : int,
                "SSH_key_setting":{
                    "checkSSHFingerprint" : true,
                    "SSHFingerprintKey" : "xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx"
                }
            }
        }
}
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
|statusCode|integer|Code issued by NetBrain server indicating the execution result.|
|statusDescription|string|The explanation of the status code.|



```python

```


```python

```


```python

```

# SNMPSetting

## GET /ServicesAPI/API/V1/CMDB/SharedDeviceSettings/SNMPSetting

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
|shareDeviceSettings.LiveHostName| string | Device hostname. |
|shareDeviceSettings.ManageIp | string | Device management IP address. |
|shareDeviceSettings.SNMP_setting| object | SNMP setting of current device. |
|shareDeviceSettings.SNMP_setting.roString| string  | value of device snmp RO.  |
|shareDeviceSettings.SNMP_setting.rwString| string | value of device snmp RWq. |
|shareDeviceSettings.SNMP_setting.snmpPort| integer | SNMP port number. |
|shareDeviceSettings.SNMP_setting.snmpVersion| integer | version number of snmp version for current device |
|shareDeviceSettings.SNMP_setting.UseCustomizedManagementIp| bool | whether current device using the customized management IP.|
|shareDeviceSettings.SNMP_setting.v3| string | Alies name. |
|shareDeviceSettings.SNMP_setting.CustomizedManagementIp| object | SNMP customized management IP setting . |
|shareDeviceSettings.SNMP_setting.CustomizedManagementIp.retrieve_CPU| string | value of customized management IP retrieve CPU. |
|shareDeviceSettings.SNMP_setting.CustomizedManagementIp.retrieve_memory| string | value of customized management IP retrieve memory. |
|shareDeviceSettings.SNMP_setting.CustomizedManagementIp.ManageIp| string | value of customized management IP. |
|shareDeviceSettings.SNMP_setting.CustomizedManagementIp.snmpVersion| string | customized SNMP version. |
|shareDeviceSettings.SNMP_setting.CustomizedManagementIp.LiveStatus| integer | SNMP setting of current device. |
|shareDeviceSettings.SNMP_setting.CustomizedManagementIp.ro| string | value of customized management IP RO. |
|shareDeviceSettings.SNMP_setting.CustomizedManagementIp.rw| string | value of customized management IP RW. |

***Example***


```python
API Body = {  
        "LiveHostName" : "CP-SW1",
        "ManageIp" : "192.168.0.58",
        "SNMP_setting" : {
          "roString": "=",
          "rwString": "=",
          "snmpVersion": 1/2/3,
          "snmpPort": 161,
          "v3": "AliesName",
          "UseCustomizedManagementIp": false,
          "CustomizedManagementIp": {
            "retrieve_CPU":"string",
            "retrieve_memory":"string",
            "ManageIp": "",
            "LiveStatus": int,
            "snmpVersion": "string",
            "ro": "string",
            "rw": "string",
            "v3": "AliesName"
          }  
        }
}
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
|statusCode|integer|Code issued by NetBrain server indicating the execution result.|
|statusDescription|string|The explanation of the status code.|


```python

```


```python

```


```python

```

# APIServerSetting

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
|shareDeviceSettings.LiveHostName*| string | Device hostname. |
|shareDeviceSettings.ManageIp* | string | Device management IP address. |
|shareDeviceSettings.API_setting| object list | API servers applied to current device. |
|shareDeviceSettings.API_setting.API_plugin| string | name of applied API plugin. |
|shareDeviceSettings.API_setting.API_server| object | applied API server. |
|shareDeviceSettings.API_setting.API_server.name| string | applied API servers name. |
|shareDeviceSettings.API_setting.API_server.front_server| string | front server connect with applied API server. |


```python
API Body = {  
        "LiveHostName" : "CP-SW1",
        "ManageIp" : "192.168.0.58",
        "API_setting" : {[
                {
                    "API_plugin" : "string",
                    "API_server" : {
                        "name" : "string"/null,
                        "front_server" : "string"/null
                    }     
                },
                {
                    "API_plugin" : "string",
                    "API_server" : {
                        "name" : "string"/null,
                        "front_server" : "string"/null
                    }  
                },
                {
                    "API_plugin" : "string",
                    "API_server" : {
                        "name" : "string"/null,
                        "front_server" : "string"/null
                    }     
                },
                .
                .
                .
            ]
        }
}
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
|statusCode|integer|Code issued by NetBrain server indicating the execution result.|
|statusDescription|string|The explanation of the status code.|


```python

```



```python

```
