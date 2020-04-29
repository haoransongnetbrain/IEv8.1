GET /ServicesAPI/API/V1/CMDB/SharedDeviceSettings
-------------------------------------------------

This API is used to get devices SSH Fingerprint Key in current domain. The
response of this API will return a list in JSON format.

Detail Information
------------------

>   **Title:** SSH Fingerprint Key API

>   **Version:** 04/27/2020

>   **API Server URL:** http(s)://IP Address of NetBrain Web API
>   Server/ServicesAPI/API/V1/CMDB/SharedDeviceSettings

>   **Authentication:**

| **Type**              | **In**  | **Name**             |
|-----------------------|---------|----------------------|
| Bearer Authentication | Headers | Authentication token |

Request body (\*required)
-------------------------

>   No request body.

Query Parameters (\*required)
-----------------------------

| **Name** | **Type**                 | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|----------|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| hostname | string OR list of string | A list of device hostnames                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ip       | string OR list of string | A list of device management IPs                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| status       | bool | Device SSH fingerprint key status, enable is true, unenable is false.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|          |                          | Hostname, ip and status can be assume as the filters, the relationship between status and hostname is AND. If provided both of hostname and ip, hostname has higher priority. If any of the devices are not found from the provided query parameter, return the found devices as a list in response and add another json key "deviceNotFound", the value is a mixed list of hostnames and IPs that are not found. If both of hostname and ip are as empty, response would depends on the "skip" and "limit" values customer insert.                                                                                                                                                  |
| skip     | integer                  | The amount of records to be skipped. The value must not be negative. If the value is negative, API throws exception {"statusCode":791001,"statusDescription":"Parameter 'skip' cannot be negative"}. No upper bound for this parameter.                                                                                                                                                                                                                                                                                                                                   |
| limit    | integer                  | The up limit amount of device records to return per API call. The value must not be negative. If the value is negative, API throws exception {"statusCode":791001,"statusDescription":"Parameter 'limit' cannot be negative"}. No upper bound for this parameter. If the parameter is not specified in API call, it means there is not limitation setting on the call.                                                                                                                                                                                                    |
|          |                          | If only provide skip value, return the device list with 50 devices information start from the skip number. If only provide limit value, return from the first device in DB. If provided both skip and limit, return as required. Error exceptions follow each parameter's description.                                                                                                                                                                                                                                                                                    |
|          |                          | Skip and limit parameters are based on the search result from DB. The "limit" value valid range is 10 - 100, if the assigned value exceeds the range, the server will respond error message: "Parameter 'limit' must be greater than or equal to 10 and less than or equal to 100."                                                                                                                                                                                                                                                                                       |

Headers
-------

>   **Data Format Headers**

| **Name**     | **Type** | **Description**            |
|--------------|----------|----------------------------|
| Content-Type | string   | support "application/json" |
| Accept       | string   | support "application/json" |

>   **Authorization Headers**

| **Name** | **Type** | **Description**                           |
|----------|----------|-------------------------------------------|
| token    | string   | Authentication token, get from login API. |

Response
--------

| **Name**                                | **Type**    | **Description**                                                 |
|-----------------------------------------|-------------|-----------------------------------------------------------------|
| statusCode                              | integer     | Code issued by NetBrain server indicating the execution result. |
| statusDescription                       | string      | The explanation of the status code.                             |
| shareDeviceSettings                     | object list | A list of device setting object.                                |
| shareDeviceSettings.hostname            | string      | Device hostname.                                                |
| shareDeviceSettings.Ip                  | string      | Device management IP address.                                   |
| shareDeviceSettings.checkSSHFingerprint | bool        | Device hostname.                                                |
| shareDeviceSettings.SSHFingerprintKey   | string      | The SSH Fingerprint Key of current device.                      |

**Example**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
{
    "shareDeviceSettings" : [
        {
            "hostname" : "US-BOS-R1",
            "ip" : "192.168.28.79",
            "checkSSHFingerprint" : true,
            "SSHFingerprintKey" : "xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx"
        },
        {
            "hostname" : "US-BOS-R2",
            "ip" : "192.168.28.80",
            "checkSSHFingerprint" : true,
            "SSHFingerprintKey" : "xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx"
        },
        {
            "hostname" : "US-BOS-R3",
            "ip" : "192.168.28.81",
            "checkSSHFingerprint" : true,
            "SSHFingerprintKey" : "xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx"
        },
        .
        .
        .
    ],
    "statusCode" : 790200,
    "statusDescription" : "Success"
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
