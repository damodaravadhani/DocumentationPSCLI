# Migration Guide for latest Az.EventHub PowerShell Module



The `Az.EventHub` PowerShell module version X.X.X of Azure PowerShell introduces improvised cmdlets for public use.

These changes are focused towards making the PowerShell use seamless for the end users.



The following example installs the latest version of the `Az.Eventhub` Azure PowerShell module.



```powershell

Install-Module -Name Az.EventHub -Repository PSGallery -Scope CurrentUser

```



See the following information for a list of changes.

Note: Add-Az

## Application Groups

### Get-AzEventHubApplicationGroup
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided to `-InputObject` parameter.

### New-AzEventHubApplicationGroup

- `-InputObject` and Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubApplicationGroupAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IApplicationGroup`.
- `-ThrottlingPolicyConfig` would change to `-Policy`.

### Set-AzEventHubApplicationGroup
- `-InputObject` and Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubApplicationGroupAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IApplicationGroup`.
- `-ThrottlingPolicyConfig` would change to `-Policy`.
- `-InputObject` parameter set would be seeing change in behaviour. Refer the example on top to know more.

### Remove-AzEventHubApplicationGroup
- `-InputObject` and Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubApplicationGroupAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IApplicationGroup`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided to `-InputObject` parameter.

## Network Rule Sets

### Set-AzEventHubNetworkRuleSet
- `-InputObject` and Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSNetworkRuleSetAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.INetworkRuleSet`.
- Parameter `-IPRule` is changing type from `Microsoft.Azure.Commands.EventHub.Models.PSNWRuleSetIpRulesAttributes[]` to `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.INwRuleSetIPRules[]`. Please use `New-AzEventHubIPRuleConfig` cmdlet to construct an in-memory object which can then be fed as input to `-IPRule`.
- Parameter `-VirtualNetworkRule` is changing type from `Microsoft.Azure.Commands.EventHub.Models.PSNWRuleSetIpRulesAttributes[]` to `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.INwRuleSetVirtualNetworkRules[]`. Please use `New-AzEventHubVirtualNetworkRuleConfig` cmdlet to construct an in-memory object which can then be fed as input to `-VirtualNetworkRule`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided to `-InputObject` parameter.
- `-InputObject` parameter set would be seeing change in behaviour. Refer the example on top to know more.

## Authorization Rules and SAS Keys

### New-AzEventHubAuthorizationRule
- Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSSharedAccessAuthorizationRuleAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IAuthorizationRule`.

### Set-AzEventHubAuthorizationRule
- `-InputObject` and Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSSharedAccessAuthorizationRuleAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IAuthorizationRule`.
- `-InputObject` parameter set would be seeing change in behaviour. Refer the example on top to know more.

### Get-AzEventHubAuthorizationRule
- Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSSharedAccessAuthorizationRuleAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IAuthorizationRule`.

### New-AzEventHubKey
- Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSListKeysAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IAccessKeys`.

### Get-AzEventHubKey
- Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSListKeysAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IAccessKeys`.

## Consumer Groups

### New-AzEventHubConsumerGroup
- Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSConsumerGroupAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IConsumerGroup`.

### Set-AzEventHubConsumerGroup
- `-InputObject` and Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSConsumerGroupAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IConsumerGroup`.
- `-InputObject` parameter set would be seeing change in behaviour. Refer the example on top to know more.

### Get-AzEventHubConsumerGroup
- `-InputObject` and Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSConsumerGroupAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IConsumerGroup`.
- Parameter `-MaxCount` is not supported and has been removed

### Remove-AzEventHubConsumerGroup
- `-InputObject` and Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSConsumerGroupAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IConsumerGroup`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

## Clusters

### New-AzEventHubCluster
- `-InputObject` and Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubClusterAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.ICluster`.
- `-ResourceId` parameter is being removed without being replaced as New-Az cmdlets have no utility of resource id.

### Set-AzEventHubCluster
- `-InputObject` and Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubClusterAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.ICluster`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.
- `-InputObject` parameter set would be seeing change in behaviour. Refer the example on top to know more.

### Get-AzEventHubCluster
- Parameter `-InputObject` and Output type have been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubClusterAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.ICluster`.

### Remove-AzEventHubCluster
- `-InputObject` and Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubClusterAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.ICluster`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

## EventHub Entity

### New-AzEventHub
- Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IEventhub`.
- `-InputObject` would be removed as New-Az cmdlets do not have utility for it.
- Parameter `-MessageRetentionInDays` would change to `-MessageRetentionInDay`

### Set-AzEventHub
- `-InputObject` and output type have been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IEventhub`. CaptureDescription class data members would be flattened and would directly be accessible as data members within Microsoft.`Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IEventhub`.
- Parameter `-MessageRetentionInDays` would change to `-MessageRetentionInDay` (this looks weird. I will request the powershell team to let us keep the plural).

### Remove-AzEventHub
- Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IEventhub`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

### Get-AzEventHub
- Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IEventhub`.
- Parameter `-MaxCount` is not supported and has been removed
- Parameter `-NamespaceObject` is being removed without being replaced.

## Private Endpoints

### Approve-AzEventHubPrivateEndpointConnection
- Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubPrivateEndpointConnectionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IPrivateEndpointConnection`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

### Deny-AzEventHubPrivateEndpointConnection
- Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubPrivateEndpointConnectionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IPrivateEndpointConnection`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

### Remove-AzEventHubPrivateEndpointConnection
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

### Get-AzEventHubPrivateEndpointConnection
- Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubPrivateEndpointConnectionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IPrivateEndpointConnection`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

## Private Links

### Get-AzEventHubPrivateLink
- Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubPrivateLinkResourceAttributes[]` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IPrivateLinkResourcesListResult`.

## Disaster Recovery Configs

### Get-AzEventHubGeoDRConfiguration
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSNamespaceAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IArmDisasterRecovery`.
- Output type of cmdlet has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSNamespaceAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IArmDisasterRecovery`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

### New-AzEventHubGeoDRConfiguration
- Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubDRConfigurationAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IArmDisasterRecovery`.
- Parameter `-InputObject` is being removed without being replaced.
- Parameter `-ResourceId` is being removed without being replaced.

### Remove-AzEventHubGeoDRConfiguration
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubDRConfigurationAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.IArmDisasterRecovery`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

### Set-AzEventHubGeoDRConfigurationBreakPair
- Parameter `-InputObject` is being removed without being replaced.
- Parameter `-ResourceId` is being removed without being replaced.

### Set-AzEventHubGeoDRConfigurationFailOver
- Parameter `-InputObject` is being removed without being replaced.
- Parameter `-ResourceId` is being removed without being replaced.

## Schema Groups

### New-AzEventHubSchemaGroup
- Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubsSchemaRegistryAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.ISchemaGroup`.

### Get-AzEventHubSchemaGroup
- Output type has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubsSchemaRegistryAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.ISchemaGroup`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

### Remove-AzEventHubSchemaGroup
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.EventHub.Models.PSEventHubsSchemaRegistryAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.EventHub.Models.Api202201Preview.ISchemaGroup`.