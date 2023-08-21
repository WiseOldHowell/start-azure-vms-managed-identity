# Start Azure VMs Managed Identity

DESCRIPTION 
This runbook connects to Azure and starts all VMs in an Azure subscription, a resource group, or a single named VM.
You can attach a recurring schedule to this runbook to run it at a specific time. 

REQUIRED
1. A Managed Identity asset (see Automation Account > Account Settings > Identity...) with RBAC permissions to start VMs.

OPTIONAL

2. A ResourceGroupName input parameter value that allows scoping the VMs to a particular resource group.
3. A VMName input parameter that allows the specification of a single VM.

NOTES
- Link Conditions to determine how to get the VMs -
Following the 'Connect AZAccount' activity there are three sequence links that have conditions set.  These conditions are mutually exclusive and will direct the workflow to only one of the connected activities to get VMs.

- Merge VMs activity -
The 'Merge VMs' activity is used to merge the output of the immediately preceding activities.  By merging the output into a single activity, which then re-outputs the objects, the downstream activities, like 'Start VM'  are able to refer to a single activity for input data.  At design time, we don't know which of the immediately preceding activities will run, so 'Start VM' doesn't know which activity to refer to for input data.  By creating 'Merge VMs', 'Start VM' has a single activity to refer to for input.

AUTHOR
- System Center Automation Team 
- Edit by WiseOldHowell

LAST EDIT
- 2023-08-21

RELEASE NOTES
- 2016-05-09 First release
- 2016-10-22 Handle changes to the output object properties from Start-AzureRmVm
- 2023-06-20 Updated with Managed Identity
- 2023-08-21 Published to GitHub


![image](https://github.com/WiseOldHowell/start-azure-vms-managed-identity/assets/25933348/9010dd4f-fc91-4ec7-aa52-cb7f55e375bf)
