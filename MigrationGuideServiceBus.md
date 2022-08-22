# Migration Guide for latest Az.ServiceBus PowerShell Module



The `Az.ServiceBus` PowerShell module version X.X.X of Azure PowerShell introduces improvised cmdlets for public use.

These changes are focused towards making the PowerShell use seamless for the end users.



The following example installs the latest version of the `Az.ServiceBus` Azure PowerShell module.



```powershell

Install-Module -Name Az.ServiceBus -Repository PSGallery -Scope CurrentUser

```
## Major Changes:

### Behavior of -InputObject: 

Until Module X.X.X, -InputObject supports passing an in memory created object to additional cmdlet in pipeline.Due to above design, updating resources becomes a multi step approeach. 

With the new module release, -InputObject behavior would be changing for a seamless experience. 

In contrast to earlier approach, -InputObject now would support object of corresponding input type as well as resource Id directly to the cmdlet.This would make cmdlet usage fairly easy and faster as compared to the old approach. 

Below example shows the difference in -InputObject Usage: 

### Before

Below example shows how to update duplicate detection on existing service bus namespace with Module version older than X.X.X 
```
$QueueObj = Get-AzServiceBusQueue -ResourceGroup Default-ServiceBus-WestUS -NamespaceName SB-Example1 -QueueName SB-Queue_example1

$QueueObj.DeadLetteringOnMessageExpiration = $True
$QueueObj.SupportOrdering = $True

Set-AzServiceBusQueue -ResourceGroup Default-ServiceBus-WestUS -NamespaceName SB-Example1 -QueueName SB-Queue_example1 -QueueObj $QueueObj
```

### After

Below example shows how to update capture description on existing event hub with starting with / after Module version  X.X.X 

```
$eventhub = Get-AzEventHub -InputObject <ResourceID of event hub>

Set-AzEventHub -InputObject $eventhub -CaptureEnabled -SizeLimitInBytes 10485763 -IntervalInSeconds 120 -Encoding Avro -DestinationName EventHubArchive.AzureBlockBlob -BlobContainer container -ArchiveNameFormat "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}" -StorageAccountResourceId "/subscriptions/{SubscriptionId}/resourceGroups/MyResourceGroupName/providers/Microsoft.ClassicStorage/storageAccounts/teststorage"


```

### Pipelining support

- Accept pipeline Input for InputObject(InputObject pipelining) can be implemented in the following manner:

```
Get-AzEventHub -InputObject <ResourceId of the eventhub> | Set-AzEventHub -MessageRetentionInDays 6

```

- Accept pipeline input for parameters (parameter pipelining) is not supported

### Positional Binding

- Positional binding is not supported. 


## Deprecation Announcements

With new release,below cmdlets are marked to be deprecated:
 - Add-AzServiceBusIPRule
 - Add-AzServiceBusVirtualNetworkRule 
 - Remove-AzServiceBusIPRule 
 - Remove-AzServiceBusVirtualNetworkRule  
 - Remove-AzServiceBusNetworkRuleSet 

Use Set-AzServiceBusNetworkRuleSet to add/remove multiple IP/ virtual network rules.


## Changes to existing Cmdlets


## Network Rule Sets

### Set-AzServiceBusNetworkRuleSet
- Input type of parameter `-InputObject` and Output type of this cmdlet have been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSNetworkRuleSetAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.INetworkRuleSet`.
- Parameter `-IPRule` is changing type from `Microsoft.Azure.Commands.ServiceBus.Models.PSNWRuleSetIpRulesAttributes[]` to `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.INwRuleSetIPRules[]`.Please use `New-AzServiceBusIPRuleConfig` cmdlet to construct an in-memory object which can then be fed as input to `-IPRule`.

- Parameter `-VirtualNetworkRule` is changing type from `Microsoft.Azure.Commands.ServiceBus.Models.PSNWRuleSetVirtualNetworkRulesAttributes[]` to `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.INwRuleSetVirtualNetworkRules[]`.Please use `New-AzServiceBusVirtualNetworkRuleConfig` cmdlet to construct an in-memory object which can then be fed as input to `-VirtualNetworkRule`.

- `-ResourceId` parameter would be deprecated. Henceforth, resource id can be provided to `-InputObject` parameter.

- `-InputObject` parameter set would have a change in behaviour. Refer the [section](#behavior-of--inputobject) to know more.

### Get-AzServiceBusNetworkRuleSet
- Input type of parameter `-InputObject` and Output type of this cmdlet have been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSNetworkRuleSetAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.INetworkRuleSet`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id can be provided to `-InputObject` parameter.

## Authorization Rules and SAS Keys

### New-AzServiceBusAuthorizationRule
- Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSSharedAccessAuthorizationRuleAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IAuthorizationRule`.

### Set-AzServiceBusAuthorizationRule
- Input type of parameter `-InputObject` and Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSSharedAccessAuthorizationRuleAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IAuthorizationRule`.
- `-InputObject` parameter set would have a change in behaviour. Refer the [section](#behavior-of--inputobject) to know more.

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
- `-SizeInBytes` and `-MessageCount` are readonly parameters and are getting removed. 
- Parameter `-EnableBatchedOperations` is renamed to `-EnableBatchedOperation`.

### Set-AzServiceBusQueue
- Input type of parameter `-InputObject` and Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSQueueAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbQueue`.
- `-InputObject` parameter set would have a change in behaviour. Refer the [section](#behavior-of--inputobject) to know more.

### Remove-AzServiceBusQueue
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSQueueAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbQueue`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id can be provided as input to `-InputObject` parameter.

### Get-AzServiceBusQueue
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSQueueAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbQueue`.
- Parameter `-MaxCount` has been removed. Use `-Skip` and `-Top` for pagination use cases.

## Topic Entity

### Get-AzServiceBusTopic
- Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSTopicAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbTopic`.
- Parameter `-MaxCount` has been removed. Use `-Skip` and `-Top` for pagination use cases.

### Set-AzServiceBusTopic
- Input type of parameter `-InputObject` and Output type of this cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSTopicAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbTopic`.
- `-InputObject` parameter set would have a change in behaviour. Refer the [section](#behavior-of--inputobject) to know more.

### New-AzServiceBusTopic
- Output type of this cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSTopicAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbTopic`.
- Parameters `-AutoDeleteOnIdle`, `-DuplicateDetectionHistoryTimeWindow`, `-DefaultMessageTimeToLive` is changing type from System.String to System.Timespan. To set time span to 3 minutes use "00:03:00". To set time span to 5 days, 3 hours use "05:00:03:00". This is not expected to break the cmdlet.
-  `-SizeInBytes` is readonly parameter and is getting removed. 
- Parameter `-EnableBatchedOperations` would be renamed to `-EnableBatchedOperation`.

### Remove-AzServiceBusTopic
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSTopicAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbTopic`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id can be provided as input to `-InputObject` parameter.

## Rule Entity

### Get-AzServiceBusRule
- Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSRulesAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IRule`.
- Parameter `-MaxCount` has been removed. Use `-Skip` and `-Top` for pagination use cases.

### Set-AzServiceBusRule
- Input type of parameter `-InputObject` and Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSRulesAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IRule`.
- `-InputObject` parameter set would have a change in behaviour. Refer the [section](#behavior-of--inputobject) to know more.

### New-AzServiceBusRule
- Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSRulesAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IRule`.
- Parameter `-RequiresPreprocessing` is being renamed to `-ActionRequiresPreprocessing`.

### Remove-AzServiceBusRule
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSRulesAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IRule`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id can be provided as input to `-InputObject` parameter.

## Subscription Entity

### Get-AzServiceBusSubscription
- Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSSubscriptionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbSubscription`.
- Parameter `-MaxCount` has been removed. Use `-Skip` and `-Top` for pagination use cases.

### New-AzServiceBusSubscription
- Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSSubscriptionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbSubscription`.


### Set-AzServiceBusSubscription
- Input type of parameter `-InputObject` and Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSSubscriptionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbSubscription`.
- `-InputObject` parameter set would have a change in behaviour. Refer the [section](#behavior-of--inputobject) to know more.

### Remove-AzServiceBusSubscription
- Input type of parameter `-InputObject` and Output type of cmdlet has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSSubscriptionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.ISbSubscription`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id can be provided as input to `-InputObject` parameter.

## Private Endpoints

### Approve-AzServiceBusPrivateEndpointConnection
- Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusPrivateEndpointConnectionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IPrivateEndpointConnection`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id can be provided as input to `-InputObject` parameter.

### Deny-AzServiceBusPrivateEndpointConnection
- Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusPrivateEndpointConnectionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IPrivateEndpointConnection`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id can be provided as input to `-InputObject` parameter.

### Remove-AzServiceBusPrivateEndpointConnection
- `-ResourceId` parameter would be deprecated. Henceforth, resource id can be provided as input to `-InputObject` parameter.

### Get-AzServiceBusPrivateEndpointConnection
- Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusPrivateEndpointConnectionAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IPrivateEndpointConnection`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id can be provided as input to `-InputObject` parameter.

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
- `-Name` parameter would be removed from `-InputObject` parameter set. Henceforth,`-InputObject` must  contain the ResourceId  of  Disaster Recovery Configuration alias.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id can be provided as input to `-InputObject` parameter.

### New-AzServiceBusGeoDRConfiguration
- Output type has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusDRConfigurationAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IArmDisasterRecovery`.
-  `-InputObject` and `-ResourceId` are not supported during resource creation, hence are being removed.

### Remove-AzServiceBusGeoDRConfiguration
- Input type of parameter `-InputObject` has been changed from `Microsoft.Azure.Commands.ServiceBus.Models.PSServiceBusDRConfigurationAttributes` to
  `Microsoft.Azure.PowerShell.Cmdlets.ServiceBus.Models.Api202201Preview.IArmDisasterRecovery`.
- `-ResourceId` parameter would be deprecated. Henceforth, resource id can be provided as input to `-InputObject` parameter.

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
