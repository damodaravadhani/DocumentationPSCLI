# Migration Guide for latest Az.ServiceBus PowerShell Module



The `Az.ServiceBus` PowerShell module version X.X.X of Azure PowerShell introduces improvised cmdlets for public use.

These changes are focused towards making the PowerShell use seamless for the end users.



The following example installs the latest version of the `Az.ServiceBus` Azure PowerShell module.



```powershell

Install-Module -Name Az.ServiceBus -Repository PSGallery -Scope CurrentUser

```



See the following information for a list of changes.

## Exceptions

Due to internal design limitations, there are few cmdlets that wouldn't have any changes currently and would continue to work as per the old design. Here is list of cmdlets that are excluded from new design as of today:
- Set-AzServiceBusNamespace, Get-AzServiceBusNamespace, New-AzServiceBusNamespace, Get-AzServiceBNamespace, New-AzServiceBusAuthorizationRuleSASToken have not yet been migrated to Autorest powershell due to technical complexity. These will continue to function as they were.
- Add-AzServiceBusIPRule, Add-AzServiceBusVirtualNetworkRule, Remove-AzServiceBusIPRule, Remove-AzServiceBusVirtualNetworkRule and Remove-AzServiceBusNetworkRuleSet would be deprecated in a future release and are hence not being migrated. Reason being that Set-AzServiceBusNetworkRuleSet can be used to add or remove multiple Ip or VirtualNetwork rules. Please raise a github issue at https://github.com/Azure/azure-powershell if you want any of the deprecated cmdlets that meet your usecase.

## Network Rule Sets

### Set-AzServiceBusNetworkRuleSet
- Input type of parameter `-InputObject` and Output type of this cmdlet have been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSNetworkRuleSetAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.INetworkRuleSet`.
- Parameter `-IPRule` is changing type from `Microsoft.Azure.Commands.ServiceBus.Models.PSNWRuleSetIpRulesAttributes[]` to `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.INwRuleSetIPRules[]`. Please use `New-AzServiceBusIPRuleConfig` cmdlet to construct an in-memory object which can then be fed as input to `-IPRule`.
- Parameter `-VirtualNetworkRule` is changing type from `Microsoft.Azure.Commands.ServiceBus.Models.PSNWRuleSetVirtualNetworkRulesAttributes[]` to `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.INwRuleSetVirtualNetworkRules[]`. Please use `New-AzServiceBusVirtualNetworkRuleConfig` cmdlet to construct an in-memory object which can then be fed as input to `-VirtualNetworkRule`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided to `-InputObject` parameter.
- `-InputObject` parameter set would be seeing change in behaviour. Refer the example on top to know more.

### Get-AzServiceBusNetworkRuleSet
- Input type of parameter `-InputObject` and Output type of this cmdlet have been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSNetworkRuleSetAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.INetworkRuleSet`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided to `-InputObject` parameter.

## Authorization Rules and SAS Keys

### New-AzServiceBusAuthorizationRule
- Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSSharedAccessAuthorizationRuleAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IAuthorizationRule`.

### Set-AzServiceBusAuthorizationRule
- Input type of parameter `-InputObject` and Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSSharedAccessAuthorizationRuleAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IAuthorizationRule`.
- `-InputObject` parameter set would be seeing change in behaviour. Refer the example on top to know more.

### Get-AzServiceBusAuthorizationRule
- Input type of parameter `-InputObject` and Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSSharedAccessAuthorizationRuleAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IAuthorizationRule`.

### New-AzServiceBusKey
- Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSListKeysAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IAccessKeys`.

### Get-AzServiceBusKey
- Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSListKeysAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IAccessKeys`.

## Queue Entity

### New-AzServiceBusQueue
- Output type of this cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSQueueAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbQueue`.
- Parameters `-AutoDeleteOnIdle`, `-DuplicateDetectionHistoryTimeWindow`, `-DefaultMessageTimeToLive` and `LockDuration` is changing type from System.String to System.Timespan. To set time span to 3 minutes use "00:03:00". To set time span to 5 days, 3 hours use "05:00:03:00". This is not expected to break the cmdlet.
- Parameters `-SizeInBytes`, `-MessageCount` are being deprecated without being replaced because these variables are readonly.
- Parameter `-EnableBatchedOperations` would be renamed to `-EnableBatchedOperation`.

### Set-AzServiceBusQueue
- Input type of parameter `-InputObject` and Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSQueueAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbQueue`.
- `-InputObject` parameter set would be seeing change in behaviour. Refer the example on top to know more.

### Remove-AzServiceBusQueue
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSQueueAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbQueue`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

### Get-AzServiceBusQueue
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSQueueAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbQueue`.
- Parameter `-MaxCount` is not supported and has been removed

## Topic Entity

### Get-AzServiceBusTopic
- Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSTopicAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbTopic`.
- Parameter `-MaxCount` is not supported and has been removed

### Set-AzServiceBusTopic
- Input type of parameter `-InputObject` and Output type of this cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSTopicAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbTopic`.
- `-InputObject` parameter set would be seeing change in behaviour. Refer the example on top to know more.

### New-AzServiceBusTopic
- Output type of this cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSTopicAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbTopic`.
- Parameters `-AutoDeleteOnIdle`, `-DuplicateDetectionHistoryTimeWindow`, `-DefaultMessageTimeToLive` is changing type from System.String to System.Timespan. To set time span to 3 minutes use "00:03:00". To set time span to 5 days, 3 hours use "05:00:03:00". This is not expected to break the cmdlet.
- Parameters `-SizeInBytes` is being deprecated without being replaced because these variables are readonly.
- Parameter `-EnableBatchedOperations` would be renamed to `-EnableBatchedOperation`.

### Remove-AzServiceBusTopic
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSTopicAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbTopic`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

## Rule Entity

### Get-AzServiceBusRule
- Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSRulesAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IRule`.
- Parameter `-MaxCount` is not supported and has been removed.

### Set-AzServiceBusRule
- Input type of parameter `-InputObject` and Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSRulesAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IRule`.
- `-InputObject` parameter set would be seeing change in behaviour. Refer the example on top to know more.

### New-AzServiceBusRule
- Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSRulesAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IRule`.
- Parameter `-RequiresPreprocessing` is being renamed to `-ActionRequiresPreprocessing`.

### Remove-AzServiceBusRule
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSRulesAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IRule`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

## Subscription Entity

### Get-AzServiceBusSubscription
- Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSSubscriptionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbSubscription`.
- Parameter `-MaxCount` is not supported and has been removed.

### New-AzServiceBusSubscription
- Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSSubscriptionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbSubscription`.
- Parameters `-AutoDeleteOnIdle`, `-LockDuration`, `-DefaultMessageTimeToLive` is changing type from System.String to System.Timespan. To set time span to 3 minutes use "00:03:00". To set time span to "5 days, 3 hours" use "05:00:03:00". This is not expected to break the cmdlet.

### Set-AzServiceBusSubscription
- Input type of parameter `-InputObject` and Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSSubscriptionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbSubscription`.
- `-InputObject` parameter set would be seeing change in behaviour. Refer the example on top to know more.

### Remove-AzServiceBusSubscription
- Input type of parameter `-InputObject` and Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSSubscriptionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbSubscription`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

## Private Endpoints

### Approve-AzServiceBusPrivateEndpointConnection
- Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusPrivateEndpointConnectionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IPrivateEndpointConnection`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

### Deny-AzServiceBusPrivateEndpointConnection
- Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusPrivateEndpointConnectionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IPrivateEndpointConnection`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

### Remove-AzServiceBusPrivateEndpointConnection
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

### Get-AzServiceBusPrivateEndpointConnection
- Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusPrivateEndpointConnectionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IPrivateEndpointConnection`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

## Private Links

### Get-AzServiceBusPrivateLink
- Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusPrivateLinkResourceAttributes[]` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IPrivateLinkResourcesListResult`.

## Disaster Recovery Configs

### Get-AzServiceBusGeoDRConfiguration
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSNamespaceAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IArmDisasterRecovery`.
- Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusDRConfigurationAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IArmDisasterRecovery`.
- `-InputObject` parameter set would also change. `-Name` parameter would be removed from this parameter set. `-InputObject` must henceforth contain the ResourceId with the alias of the Disaster Recovery Configuration. We will also release a detailed documentation of how to use the cmdlet with the breaking change release.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

### New-AzServiceBusGeoDRConfiguration
- Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusDRConfigurationAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IArmDisasterRecovery`.
- Parameter `-InputObject` is being removed without being replaced.
- Parameter `-ResourceId` is being removed without being replaced.

### Remove-AzServiceBusGeoDRConfiguration
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusDRConfigurationAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IArmDisasterRecovery`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id's can be provided as input to `-InputObject` parameter.

### Set-AzServiceBusGeoDRConfigurationBreakPair
- Parameter `-ResourceId` is being removed. Henceforth, resource id can be provided as input to `-InputObject`.

### Set-AzServiceBusGeoDRConfigurationFailOver
- Parameter `-ResourceId` is being removed. Henceforth, resource id can be provided as input to `-InputObject`.

## Migration Configurations
### Complete-AzServiceBusMigration
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusDRConfigurationAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IMigrationConfigProperties`.
- Parameter `-ResourceId` is being removed. Henceforth, resource id can be provided as input to `-InputObject`.

### Get-AzServiceBusMigration
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusMigrationConfigurationAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IMigrationConfigProperties`.
- Output type of the cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusMigrationConfigurationAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IMigrationConfigProperties`.

### Start-AzServiceBusMigration
- Output type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusMigrationConfigurationAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IMigrationConfigProperties`.

### Remove-AzServiceBusMigration
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusDRConfigurationAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IMigrationConfigProperties`.

### Stop-AzServiceBusMigration
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusDRConfigurationAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IMigrationConfigProperties`.
- Parameter `-ResourceId` is being removed. Henceforth, resource id can be provided as input to `-InputObject`.
