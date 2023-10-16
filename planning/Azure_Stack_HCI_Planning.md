[catalog]:https://azurestackhcisolutions.azure.microsoft.com/#/catalog
[switchrequirements]:https://learn.microsoft.com/en-us/azure-stack/hci/concepts/physical-network-requirements?tabs=overview%2C22H2reqs#network-switch-requirements
[requiredrules]:https://learn.microsoft.com/en-us/azure-stack/hci/concepts/firewall-requirements#required-firewall-urls
[recommendedrules]:https://learn.microsoft.com/en-us/azure-stack/hci/concepts/firewall-requirements#required-firewall-urls
[additionalrules]:https://learn.microsoft.com/en-us/azure-stack/hci/concepts/firewall-requirements#firewall-requirements-for-additional-azure-services
[internalrules]:https://learn.microsoft.com/en-us/azure-stack/hci/concepts/firewall-requirements#firewall-requirements-for-internal-rules-and-ports
[azurerequirements]:https://learn.microsoft.com/en-us/azure-stack/hci/concepts/system-requirements?tabs=azure-public#azure-requirements
[validatedswitched]:https://learn.microsoft.com/en-us/azure-stack/hci/concepts/physical-network-requirements?tabs=overview%2C22H2reqs#network-switches-for-azure-stack-hci
[enviromentchecker]:https://learn.microsoft.com/en-us/azure-stack/hci/manage/use-environment-checker?tabs=connectivity


# Welcome Kit -- Azure Stack HCI -- Planning - Draft


Welcome to the \"Azure Stack HCI -- Planning FAQ Welcome Kit.\" This
comprehensive guide is designed to provide you with essential insights
into the areas of focus and consideration when planning and designing
your Azure Stack HCI Deployment. As part of your preparation before
engaging with Microsoft engineers, this resource aims to demystify these
technologies, offering clear explanations and answers to frequently
asked questions. Whether you\'re new to these concepts or seeking to
deepen your understanding, this Welcome Kit is your stepping stone to
navigating the world of modern cloud-native solutions. 

## Requirements

As Azure Stack is a Hybrid Solution then this touches a number of areas
which normal Azure Deployments don't and in turn touches areas which a
traditional on-premises would not. In the following sections the
requirements across both will be discussed.

### Host Hardware Requirements

With Azure Stack HCI there are 2 options when selecting the hardware to
use as part of the deployment. Working with a Hardware OEM they can
provide either a Validated or an Integrated system. With the Validate
System all the hardware has been tested and validated to support Azure
Stack HCI and will be delivered just as the base hardware and will
require the firmware, operating system and drivers to be installed by
the customer/partner. With the Integrated System again the hardware has
been tested and validated to support Azure Stack HCI but with these
systems the firmware, operating system, and drivers to be pre-installed.

Details about the these systems is available within the [HCI
Catalog][catalog]
and can be used as a foundation to go into the discussions with Hardware
OEM's to find the correct hardware for your requirements.

### Network Switch Requirements

As Azure Stack HCI is a hyper-converged platform the physical network
which links the nodes together and to the rest of the network are very
important to help deliver the performance and availability required.
Depending on the purpose of the of the switch, whether it be dedicated
for management, storage or compute, or indeed for multiple of these
roles then they need to support certain [industry standards][switchrequirements].

Additionally, certain switch vendors have worked with Microsoft to
[validated their switches][validatedswitched] for each of these roles

Despite this list being available you are free to use any switch as long
as it meets the requirements for the relevant role (e.g. for a switch
used for the storage then all of the storage required standards are
needed)

### Active Directory Requirements

As the Azure Stack HCI cluster is a Windows Failover Cluster Instance
running Hyper-V and S2D then an Active Directory Domain Servers are
required. Additional once the cluster is deployed it is advised to grant
the cluster computer object permissions to the OU which the nodes and
cluster computer object are within. This is needed to allow for the
creation and modification to AD objects when roles and services are
deployed on the cluster. Also it would be recommended to disabled GPO
inheritance and then only apply the GPO's specific to Azure Stack HCI.

Sometimes these types of changed are not appropriate so there is the
option to use a fabric domain which will allow more "flexibility" to
these changes as it is limited to your Azure Stack HCI cluster(s).

The final point around the AD requirements is that AD is required to
allow the cluster to actually start so this means that, domain
controllers can run on the Azure Stack HCI cluster there needs to be
Domain Controllers reachable from the nodes when they boot.

### Azure Requirements

Azure Stack HCI required to be registered with an Azure subscription and
then synchronize with Azure at a minimum of every 28 days to allow full
cluster functionality. The [registration requirements][azurerequirements] are only certain regions are supported, these regions only hold "metadata" about your cluster and no data from the service running on Azure Stack HCI is stored in this region.

### Firewall Requirements

As part of the hybrid capabilities of Azure Stack HCI then there are
required to be a number of firewall ports and addresses which need to be
allow. The following documents list out those that are required,
recommended and those for additional services such as AKS, ARC VM
Management, etc

-   [Required Rules][requiredrules]

-   [Recommended Rules][recommendedrules]

-   [Additional Services][additionalrules]

In addition to these firewall rules for the outbound internet access
there are [rules required for internal traffic flows][internalrules], such as between
nodes and with management machines, DC's ectc. 

## Environment Validation

Once the all of the above requirements are met then they can be
validated using the [Environment Checker][enviromentchecker] can then be used to validate the
following:

-   **Connectivity validator**. Checks whether each server in the
    cluster meets the connectivity requirements. For example, each
    server in the cluster has internet connection and can connect via
    HTTPS outbound traffic to well-known Azure endpoints through all
    firewalls and proxy servers.

-   **Hardware validator**. Checks whether your hardware meets the
    system requirements. For example, all the servers in the cluster
    have the same manufacturer and model.

-   **Active Directory validator**. Checks whether the Active Directory
    preparation tool is run prior to running the deployment.

-   **Network validator**. Validates your network infrastructure for
    valid IP ranges provided by customers for deployment. For example,
    it checks there are no active hosts on the network using the
    reserved IP range.

-   **Arc integration validator**. Checks if the Azure Stack HCI cluster
    meets all the prerequisites for successful Arc onboarding.


## SDN

### SDN Planning

## Quorum

### Cluster Quorum

### Storage Pool Quorum