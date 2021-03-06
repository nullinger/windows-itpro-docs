---
title: Get alert information by ID API
description: Retrieves an alert by its ID.
keywords: apis, graph api, supported apis, get, alert, information, id
search.product: eADQiWindows 10XVcnh
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
ms.author: macapara
author: mjcaparas
ms.localizationpriority: medium
ms.date: 12/08/2017
---

# Update alert 
**Applies to:**

- Windows Defender Advanced Threat Protection (Windows Defender ATP)


[!include[Prerelease information](prerelease.md)]
Update the properties of an alert entity.

## Permissions
One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Windows Defender ATP APIs](apis-intro.md)

Permission type |	Permission	|	Permission display name
:---|:---|:---
Application |	Alerts.ReadWrite.All |	'Read and write all alerts'
Delegated (work or school account) | Alert.ReadWrite | 'Read and write alerts'

>[!Note]
> When obtaining a token using user credentials:
>- The user needs to have at least the following role permission: 'Alerts investigation' (See [Create and manage roles](user-roles-windows-defender-advanced-threat-protection.md) for more information)
>- The user needs to have access to the machine associated with the alert, based on machine group settings (See [Create and manage machine groups](machine-groups-windows-defender-advanced-threat-protection.md) for more information)

## HTTP request
```
PATCH /api/alerts/{id}
```

## Request headers

Name | Type | Description
:---|:---|:---
Authorization | String | Bearer {token}. **Required**.
Content-Type | String | application/json. **Required**.


## Request body
In the request body, supply the values for the relevant fields that should be updated.Existing properties that are not included in the request body will maintain their previous values or be recalculated based on changes to other property values. For best performance you shouldn't include existing values that haven't change.

Property | Type | Description
:---|:---|:---
status | String | Specifies the current status of the alert. The property values are: 'New', 'InProgress' and 'Resolved'.
assignedTo | String | Owner of the alert
classification | String | Specifies the specification of the alert. The property values are: 'Unknown', 'FalsePositive', 'TruePositive'. 
determination | String | Specifies the determination of the alert. The property values are: 'NotAvailable', 'Apt', 'Malware', 'SecurityPersonnel', 'SecurityTesting', 'UnwantedSoftware', 'Other'


## Response
If successful, this method returns 200 OK, and the [alert](alerts-windows-defender-advanced-threat-protection-new.md) entity in the response body with the updated properties. If alert with the specified id was not found - 404 Not Found.


## Example

**Request**

Here is an example of the request.

[!include[Improve request performance](improverequestperformance-new.md)]

```
PATCH https://api.securitycenter.windows.com/api/alerts/636688558380765161_2136280442
Content-Type: application/json
{
	"assignedTo": "Our designated secop"
}
```

**Response**

Here is an example of the response.

```
{
    "@odata.context": "https://api.securitycenter.windows.com/api/$metadata#Alerts/$entity",
    "id": "636688558380765161_2136280442",
    "severity": "Medium",
    "status": "InProgress",
    "description": "An anomalous memory operation appears to be tampering with a process associated with the Windows Defender EDR sensor.",
    "recommendedAction": "A. Validate the alert.\n1. Examine the process involved in the memory operation to determine whether the process and the observed activities are normal. \n2. Check for other suspicious activities in the machine timeline.\n3. Locate unfamiliar processes in the process tree. Check files for prevalence, their locations, and digital signatures.\n4. Submit relevant files for deep analysis and review file behaviors. \n5. Identify unusual system activity with system owners. \n\nB. Scope the incident. Find related machines, network addresses, and files in the incident graph. \n\nC. Contain and mitigate the breach. Stop suspicious processes, isolate affected machines, decommission compromised accounts or reset passwords, block IP addresses and URLs, and install security updates.\n\nD. Contact your incident response team, or contact Microsoft support for investigation and remediation services.",
    "alertCreationTime": "2018-08-07T10:18:04.2665329Z",
    "category": "Installation",
    "title": "Possible sensor tampering in memory",
    "threatFamilyName": null,
    "detectionSource": "WindowsDefenderAtp",
    "classification": null,
    "determination": null,
    "assignedTo": "Our designated secop",
    "resolvedTime": null,
    "lastEventTime": "2018-08-07T10:14:35.470671Z",
    "firstEventTime": "2018-08-07T10:14:35.470671Z",
    "actorName": null,
    "machineId": "a2250e1cd215af1ea2818ef8d01a564f67542857"
}
```
