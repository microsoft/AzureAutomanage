# Azure Automanage VM Best Practices - Linux Private Preview
Thank you for your interest in the private preview of Azure Automanage VM Best Practices for Linux! This document contains a brief overview of Azure Automanage on Linux, steps to get started with the Linux private preview, and known limitations that will be resolved during private preview. If you have any questions or feedback, feel free to email Alfred Sin (alsin@microsoft.com),  Dean Wells (deanwe@microsoft.com), or Meagan McCrory (memccror@microsoft.com). 

If you don't want to read this doc and want to get started with the preview, visit this link to get started in the Azure portal: https://aka.ms/amvmlinuxenable

## Azure Automanage
Azure Automanage for VMs is a service that eliminates the need to discover, know how to onboard, and know how to configure certain services in Azure that would benefit your virtual machine. These services help enhance reliability, security, and management for virtual machines and are considered to be Azure best practices services. 
Automanage VM Best Practices is available through two different configuration profiles: dev/test and production. The services you are onboarded to are determined by the configuration profile you choose. 
Azure Automanage is currently in public preview for Windows Server VMs and private preview for Linux VMs. Many more details about Automanage (including details on configuration profiles) can be found in our [public documentation](https://docs.microsoft.com/azure/automanage/automanage-virtual-machines). The rest of this document assumes a small degree of familiarity with the Automanage service (skimming the docs will suffice). 

## Supported Linux distributions
At the time of writing, Automanage for Linux supports the following Linux distributions:
-	CentOS 7.3+
-	RHEL 7.4-7.8
-	Ubuntu 16.04 and 18.04
-	SLES 12

This document will be updated as more distros are supported.

## Services enabled
Automanage for Linux will onboard VMs to the following services:
-	Azure Backup
-	Azure Security Center (free tier only)
-	Azure VM Insights Monitoring
-	Change Tracking
-	Inventory
-	Guest Configuration with the Linux security baseline applied in audit-only mode
-	Azure Update Management
-	Azure Automation Account
-	Log Analytics Workspace

This document will be updated as more services are added to Automanage.

It is worth noting that while Microsoft Antimalware is included for Windows Server VMs, Automanage for Linux will not onboard to the Microsoft Antimalware service (it does not have Linux support). We using your own antimalware solution.
It is also worth noting that while Guest Configuration will apply the Linux security baseline, it will only audit for compliance. Any noncompliance with the baseline will not be automatically remediated. Automatic remediation is planned to be delivered before Automanage becomes generally available. More details are available in the Known limitations section of this document.
The table below shows a summary of services onboarded to for each configuration profile for both Linux and Windows. 
 
## Getting started with Automanage for Linux
While in private preview, Automanage for Linux is currently only accessible using a custom portal link. Use the following link to access the private preview in the Azure portal:

### https://aka.ms/amvmlinuxenable

Once you have reached the Azure portal from the link above, the onboarding process is the exact same as for a Windows VM:
1.	Search for “Automanage” in the portal
 

1.	Click “Enable on existing VM” on the top left
 

1.	Click on “Select machines” in the following blade
 

1.	In the pane that pops up, you will be able to select your Linux VMs to onboard to Automanage. If you do not your Linux VMs in the list, double check that you are using the private preview link above to access Automanage in the portal. You will notice “microsoft_azure_automanagedvirtualmachines_linuxEnable=true” in your portal URL if you are using the private preview link.
If you still to not see your Linux VMs in the list, they may not be located in a supported location. More details are available in the prerequisites [here](https://docs.microsoft.com/azure/automanage/automanage-virtual-machines#prerequisites) (ignore the Windows Server prerequisite). 
You may click on the “Show ineligible virtual machines” checkbox to show Linux VMs that are in an unsupported location.
 

1.	Hit Select, choose your configuration profile (if you want backup and monitoring, choose Production), and hit Enable.

## Known limitations of private preview
1.	At the time of writing of this document, ineligible Linux distributions are not filtered out automatically. Please ensure that the VM you are onboarding is running a supported Linux distribution. We are actively working to include unsupported distributions in the eligibility UI and expect this will be resolved during the private preview timeframe. If you do try to onboard an unsupported distribution, be aware that some best practices services may not be properly configured for your VM.
1.	Guest Configuration will apply the AzureLinuxBaseline to your VM in audit-only mode, and will not attempt to remediate any non-compliance. In other words, you will be able to view the applied baseline on your VM via Guest Assignments in the portal, but non-compliant items won’t automatically be fixed for you. You will need to manually remediate if you would like to be aligned with the Azure Linux baseline. Automatic remediation is planned for delivery before Automanage is generally available. More details about Guest Configuration are available here.
1.	Currently, once onboarded, the Automanage backend does not check your VM(s) draft status. In other words, if your configuration drifts away from the recommended best practices configuration, Automanage is unable to bring it back into conformance. This functionality is code-complete and is currently rolling out. We expect rollout to complete within a week or two of the time of writing.

## Feedback
The private preview phase is the perfect time for you to influence the direction of Automanage for Linux as we work to bring it to the public preview and GA phases. Feel free to reach out to Alfred Sin (alsin@microsoft.com),  Dean Wells (deanwe@microsoft.com), or Meagan McCrory (memccror@microsoft.com) with any questions or feedback at any point in time.
