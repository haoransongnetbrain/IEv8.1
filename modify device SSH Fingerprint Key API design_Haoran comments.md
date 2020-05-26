PUT/ServicesAPI/API/V1/CMDB/SharedDeviceSettings
------------------------------------------------

This API is used to update devices SSH Fingerprint Key in current domain.

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

| **Name**                                  | **Type**    | **Description**                                          |
|-------------------------------------------|-------------|----------------------------------------------------------|
| shareDeviceSettings                       | object list | A list of device setting object.                         |
| shareDeviceSettings.hostname\*            | string      | Device hostname.                                         |
| shareDeviceSettings.Ip                    | string      | Device management IP address.                            |
| shareDeviceSettings.checkSSHFingerprint\* | bool        | Verify SSH Fingerprint Key status to be updated.         |
| shareDeviceSettings.SSHFingerprintKey\*   | string      | The SSH Fingerprint Key of current device to be updated. |

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
input_body = {
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
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Query Parameters (\*required)
-----------------------------

>   No query parameter required.

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

| **Name**          | **Type** | **Description**                                                 |
|-------------------|----------|-----------------------------------------------------------------|
| statusCode        | integer  | Code issued by NetBrain server indicating the execution result. |
| statusDescription | string   | The explanation of the status code.                             |

**Example**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
### Success response:
{
    "statusCode" : 790200,
    "statusDescription" : "Success"
}

### partially success:
{
    "statusCode" : 790xxx,
    "statusDescription" : "Devices [...] not found."
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    "statusDescription" : "Update on devices [...] failed. <Reason>"
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
