# Virtual WANs `[Microsoft.Network/virtualWans]`

This module deploys a Virtual WAN.

## Navigation

- [Resource types](#Resource-types)
- [Parameters](#Parameters)
- [Outputs](#Outputs)
- [Cross-referenced modules](#Cross-referenced-modules)
- [Deployment examples](#Deployment-examples)

## Resource types

| Resource Type | API Version |
| :-- | :-- |
| `Microsoft.Authorization/locks` | [2020-05-01](https://learn.microsoft.com/en-us/azure/templates/Microsoft.Authorization/2020-05-01/locks) |
| `Microsoft.Authorization/roleAssignments` | [2022-04-01](https://learn.microsoft.com/en-us/azure/templates/Microsoft.Authorization/2022-04-01/roleAssignments) |
| `Microsoft.Network/virtualWans` | [2023-04-01](https://learn.microsoft.com/en-us/azure/templates/Microsoft.Network/2023-04-01/virtualWans) |

## Parameters

**Required parameters**

| Parameter Name | Type | Description |
| :-- | :-- | :-- |
| `name` | string | Name of the Virtual WAN. |

**Optional parameters**

| Parameter Name | Type | Default Value | Allowed Values | Description |
| :-- | :-- | :-- | :-- | :-- |
| `allowBranchToBranchTraffic` | bool | `False` |  | True if branch to branch traffic is allowed. |
| `allowVnetToVnetTraffic` | bool | `False` |  | True if VNET to VNET traffic is allowed. |
| `disableVpnEncryption` | bool | `False` |  | VPN encryption to be disabled or not. |
| `enableDefaultTelemetry` | bool | `True` |  | Enable telemetry via a Globally Unique Identifier (GUID). |
| `location` | string | `[resourceGroup().location]` |  | Location where all resources will be created. |
| `lock` | string | `''` | `['', CanNotDelete, ReadOnly]` | Specify the type of lock. |
| `roleAssignments` | array | `[]` |  | Array of role assignment objects that contain the 'roleDefinitionIdOrName' and 'principalId' to define RBAC role assignments on this resource. In the roleDefinitionIdOrName attribute, you can provide either the display name of the role definition, or its fully qualified ID in the following format: '/providers/Microsoft.Authorization/roleDefinitions/c2f4ef07-c644-48eb-af81-4b1b4947fb11'. |
| `tags` | object | `{object}` |  | Tags of the resource. |
| `type` | string | `'Standard'` | `[Basic, Standard]` | The type of the Virtual WAN. |


### Parameter Usage: `roleAssignments`

Create a role assignment for the given resource. If you want to assign a service principal / managed identity that is created in the same deployment, make sure to also specify the `'principalType'` parameter and set it to `'ServicePrincipal'`. This will ensure the role assignment waits for the principal's propagation in Azure.

<details>

<summary>Parameter JSON format</summary>

```json
"roleAssignments": {
    "value": [
        {
            "roleDefinitionIdOrName": "Reader",
            "description": "Reader Role Assignment",
            "principalIds": [
                "12345678-1234-1234-1234-123456789012", // object 1
                "78945612-1234-1234-1234-123456789012" // object 2
            ]
        },
        {
            "roleDefinitionIdOrName": "/providers/Microsoft.Authorization/roleDefinitions/c2f4ef07-c644-48eb-af81-4b1b4947fb11",
            "principalIds": [
                "12345678-1234-1234-1234-123456789012" // object 1
            ],
            "principalType": "ServicePrincipal"
        }
    ]
}
```

</details>

<details>

<summary>Bicep format</summary>

```bicep
roleAssignments: [
    {
        roleDefinitionIdOrName: 'Reader'
        description: 'Reader Role Assignment'
        principalIds: [
            '12345678-1234-1234-1234-123456789012' // object 1
            '78945612-1234-1234-1234-123456789012' // object 2
        ]
    }
    {
        roleDefinitionIdOrName: '/providers/Microsoft.Authorization/roleDefinitions/c2f4ef07-c644-48eb-af81-4b1b4947fb11'
        principalIds: [
            '12345678-1234-1234-1234-123456789012' // object 1
        ]
        principalType: 'ServicePrincipal'
    }
]
```

</details>
<p>

### Parameter Usage: `tags`

Tag names and tag values can be provided as needed. A tag can be left without a value.

<details>

<summary>Parameter JSON format</summary>

```json
"tags": {
    "value": {
        "Environment": "Non-Prod",
        "Contact": "test.user@testcompany.com",
        "PurchaseOrder": "1234",
        "CostCenter": "7890",
        "ServiceName": "DeploymentValidation",
        "Role": "DeploymentValidation"
    }
}
```

</details>

<details>

<summary>Bicep format</summary>

```bicep
tags: {
    Environment: 'Non-Prod'
    Contact: 'test.user@testcompany.com'
    PurchaseOrder: '1234'
    CostCenter: '7890'
    ServiceName: 'DeploymentValidation'
    Role: 'DeploymentValidation'
}
```

</details>
<p>

## Outputs

| Output Name | Type | Description |
| :-- | :-- | :-- |
| `location` | string | The location the resource was deployed into. |
| `name` | string | The name of the virtual WAN. |
| `resourceGroupName` | string | The resource group the virtual WAN was deployed into. |
| `resourceId` | string | The resource ID of the virtual WAN. |

## Cross-referenced modules

_None_

## Deployment examples

The following module usage examples are retrieved from the content of the files hosted in the module's `.test` folder.
   >**Note**: The name of each example is based on the name of the file from which it is taken.

   >**Note**: Each example lists all the required parameters first, followed by the rest - each in alphabetical order.

<h3>Example 1: Common</h3>

<details>

<summary>via Bicep module</summary>

```bicep
module virtualWan './network/virtual-wan/main.bicep' = {
  name: '${uniqueString(deployment().name, location)}-test-nvwcom'
  params: {
    // Required parameters
    name: 'nvwcom001'
    // Non-required parameters
    allowBranchToBranchTraffic: true
    allowVnetToVnetTraffic: true
    disableVpnEncryption: true
    enableDefaultTelemetry: '<enableDefaultTelemetry>'
    lock: 'CanNotDelete'
    roleAssignments: [
      {
        principalIds: [
          '<managedIdentityPrincipalId>'
        ]
        principalType: 'ServicePrincipal'
        roleDefinitionIdOrName: 'Reader'
      }
    ]
    tags: {
      Environment: 'Non-Prod'
      Role: 'DeploymentValidation'
    }
    type: 'Basic'
  }
}
```

</details>
<p>

<details>

<summary>via JSON Parameter file</summary>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    // Required parameters
    "name": {
      "value": "nvwcom001"
    },
    // Non-required parameters
    "allowBranchToBranchTraffic": {
      "value": true
    },
    "allowVnetToVnetTraffic": {
      "value": true
    },
    "disableVpnEncryption": {
      "value": true
    },
    "enableDefaultTelemetry": {
      "value": "<enableDefaultTelemetry>"
    },
    "lock": {
      "value": "CanNotDelete"
    },
    "roleAssignments": {
      "value": [
        {
          "principalIds": [
            "<managedIdentityPrincipalId>"
          ],
          "principalType": "ServicePrincipal",
          "roleDefinitionIdOrName": "Reader"
        }
      ]
    },
    "tags": {
      "value": {
        "Environment": "Non-Prod",
        "Role": "DeploymentValidation"
      }
    },
    "type": {
      "value": "Basic"
    }
  }
}
```

</details>
<p>

<h3>Example 2: Min</h3>

<details>

<summary>via Bicep module</summary>

```bicep
module virtualWan './network/virtual-wan/main.bicep' = {
  name: '${uniqueString(deployment().name, location)}-test-nvwmin'
  params: {
    // Required parameters
    name: 'nvwmin001'
    // Non-required parameters
    enableDefaultTelemetry: '<enableDefaultTelemetry>'
  }
}
```

</details>
<p>

<details>

<summary>via JSON Parameter file</summary>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    // Required parameters
    "name": {
      "value": "nvwmin001"
    },
    // Non-required parameters
    "enableDefaultTelemetry": {
      "value": "<enableDefaultTelemetry>"
    }
  }
}
```

</details>
<p>