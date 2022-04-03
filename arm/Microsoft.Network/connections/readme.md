# Virtual Network Gateway Connections `[Microsoft.Network/connections]`

This template deploys a virtual network gateway connection.

## Navigation

- [Resource types](#Resource-types)
- [Parameters](#Parameters)
- [Outputs](#Outputs)
- [Template references](#Template-references)

## Resource types

| Resource Type | API Version |
| :-- | :-- |
| `Microsoft.Authorization/locks` | 2017-04-01 |
| `Microsoft.Network/connections` | 2021-05-01 |

## Parameters

**Required parameters**
| Parameter Name | Type | Description |
| :-- | :-- | :-- |
| `localVirtualNetworkGatewayName` | string | Specifies the local Virtual Network Gateway name |
| `name` | string | Remote connection name |
| `remoteEntityName` | string | Specifies the remote Virtual Network Gateway/ExpressRoute |

**Optional parameters**
| Parameter Name | Type | Default Value | Allowed Values | Description |
| :-- | :-- | :-- | :-- | :-- |
| `customIPSecPolicy` | object | `{object}` |  | The IPSec Policies to be considered by this connection |
| `enableBgp` | bool | `False` |  | Value to specify if BGP is enabled or not |
| `enableDefaultTelemetry` | bool | `True` |  | Enable telemetry via the Customer Usage Attribution ID (GUID). |
| `location` | string | `[resourceGroup().location]` |  | Location for all resources. |
| `lock` | string | `'NotSpecified'` | `[CanNotDelete, NotSpecified, ReadOnly]` | Specify the type of lock. |
| `remoteEntityResourceGroup` | string | `''` |  | Remote Virtual Network Gateway/ExpressRoute resource group name |
| `remoteEntitySubscriptionId` | string | `''` |  | Remote Virtual Network Gateway/ExpressRoute Subscription ID |
| `routingWeight` | string | `''` |  | The weight added to routes learned from this BGP speaker. |
| `tags` | object | `{object}` |  | Tags of the resource. |
| `usePolicyBasedTrafficSelectors` | bool | `False` |  | Enable policy-based traffic selectors |
| `virtualNetworkGatewayConnectionType` | string | `'Ipsec'` | `[Ipsec, VNet2VNet, ExpressRoute, VPNClient]` | Gateway connection type. |
| `vpnSharedKey` | string | `''` |  | Specifies a VPN shared key. The same value has to be specified on both Virtual Network Gateways |


### Parameter Usage: `customIPSecPolicy`

If ipsecEncryption parameter is empty, customIPSecPolicy will not be deployed. The parameter file should look like below.

```json
"customIPSecPolicy": {
    "value": {
        "saLifeTimeSeconds": 0,
        "saDataSizeKilobytes": 0,
        "ipsecEncryption": "",
        "ipsecIntegrity": "",
        "ikeEncryption": "",
        "ikeIntegrity": "",
        "dhGroup": "",
        "pfsGroup": ""
    }
},
```

Format of the full customIPSecPolicy parameter in parameter file.

```json
"customIPSecPolicy": {
    "value": {
        "saLifeTimeSeconds": 28800,
        "saDataSizeKilobytes": 102400000,
        "ipsecEncryption": "AES256",
        "ipsecIntegrity": "SHA256",
        "ikeEncryption": "AES256",
        "ikeIntegrity": "SHA256",
        "dhGroup": "DHGroup14",
        "pfsGroup": "None"
    }
},
```

### Parameter Usage: `tags`

Tag names and tag values can be provided as needed. A tag can be left without a value.

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

## Outputs

| Output Name | Type | Description |
| :-- | :-- | :-- |
| `name` | string | The name of the remote connection |
| `resourceGroupName` | string | The resource group the remote connection was deployed into |
| `resourceId` | string | The resource ID of the remote connection |

## Template references

- [Connections](https://docs.microsoft.com/en-us/azure/templates/Microsoft.Network/2021-05-01/connections)
- [Locks](https://docs.microsoft.com/en-us/azure/templates/Microsoft.Authorization/2017-04-01/locks)
