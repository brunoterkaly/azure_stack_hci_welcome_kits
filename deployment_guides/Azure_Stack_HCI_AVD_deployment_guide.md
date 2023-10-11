# AVD Deployment Guides On Azure Stack HCI  
This is a step-by-step guide on how to deploy and configure Azure Virtual Desktop (AVD) on Azure Stack HCI, ensuring an optimized user experience.  

>**Important Note**: As for now (Oct 2023) AVD on HCI (22H2) is in preview, i.e. things will change so please be prepared and consult this document for future changes.  
[Azure Virtual Desktop for Azure Stack HCI overview (preview)](https://learn.microsoft.com/en-us/azure/virtual-desktop/azure-stack-hci-overview)

## Requirements (For AVD On Azure Stack HCI)
Prior planning an installation visit [Set up Azure Virtual Desktop for Azure Stack HCI (preview)](https://learn.microsoft.com/en-us/azure/virtual-desktop/azure-stack-hci#prerequisites) to see the prerequisites for AVD on HCI.  
Most important: You need...
- a registered working Azure Stack HCI cluster 
- have an Active Directory sync'ed with your Microsoft Entra ID (formerly known as Azure Active Directory) 
- a valid Azure subscription with owner privileges.
  
## Currently There Are 2 Options Of Deploying AVD On HCI Possible:##  
Both have pros and cons and might (will) change in the future. 
1. Option 1: Will provide you automation via the Azure Portal (Azure Arc). I.e. you can create AVD desktop VMs hosted on your Azure Stack HCI using the portal wizard or an ARM template. For this to work you need to enable *Azure Arc VM management* by installing a feature called *Azure Resource Bridge*. This requires time, planning and maintenance. The idea will last but the process of installation will change when HCI 23H2 is released. Do this when you want to learn how the final experience could look like, love Kubernetes, require automation (e.g. ARM) and are ready to redo.

2. Option 2: The Manual Process will get you fast to have an AVD desktop hosted on your HCI. You will learn what it takes and have most freedom of choice / control. Creating a lot of AVD desktops can be teadious with this approach although a lot of steps can (you) be automated with scripting. Do this when you need to be fast - want to avoid friction and focus on AVD on HCI.

## Option 1: Automated Via The Azure Portal (Azure Arc) Using Azure Arc VM management (aka Azure Resource Bridge)
[What is Azure Arc VM management? (preview)](https://learn.microsoft.com/en-us/azure-stack/hci/manage/azure-arc-vm-management-overview)

[Set up Azure Virtual Desktop for Azure Stack HCI (preview)](https://learn.microsoft.com/en-us/azure/virtual-desktop/azure-stack-hci)

## Option 2: Manual Process
- (optional) Optimize image e.g. convert to dynamically expanding vhdx to save disk space.
- (optional - but likely) Create a VM for golden image creation: E.g. to run windows update, install your language packs, applications, - frameworks, runtimes -> sysprep (!!!important!!! using: mode:vm) -> Checkpoint for later re-use.
- Note: Only install what will 'survive' a sysprep (e.g. don't do ARC Agent nor AVD Hostpool registration yet)
- 
- (optional) FSLogix: Prepare a SMB file share (provide profile share with correct ACLs)
- (optional) FSLogix: Prepare a GPO for the AD OrgUnit (OU) the VDIs will be joined to.
- Deploy a empty AVD Hostpool in Azure.
- Create a Application Group for this Hostpool and allow an AAD User Group access to it.
- Create a Workspace containing the App Group created before.
- Deploy a VDI VM on HCI using the VDI image (from vhdx obtained in 1./2. or 3.)
- Deploy the AVD Agents into the VDI VM
- Deploy the Remote Desktop App for the User
- (When using Win 10|11 multisession) - Enable Azure Benefits
- (optional) when you are using proxies for the session hosts.
- (optional) Publish NotepadPlusPlus in your AVD Application Group