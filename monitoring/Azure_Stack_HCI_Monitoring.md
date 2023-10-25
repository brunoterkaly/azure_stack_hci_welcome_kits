[arcenabledservers]:https://learn.microsoft.com/en-us/azure/azure-arc/servers/overview
[connectedmachineagent]:https://learn.microsoft.com/en-us/azure/azure-arc/servers/agent-overview
[ama]:https://learn.microsoft.com/en-us/azure/azure-monitor/agents/agents-overview

# Welcome Kit - Azure Stack HCI - Monitoring - Draft


Welcome to the "Azure Stack HCI - Monitoring Welcome Kit." This
comprehensive guide is designed to provide you with essential insights
into the areas of focus and consideration when planning and designing
your Azure Stack HCI Monitoring. As part of your preparation before
engaging with Microsoft engineers, this resource aims to demystify these
technologies, offering clear explanations and answers to frequently
asked questions. Whether you're new to these concepts or seeking to
deepen your understanding, this Welcome Kit is your stepping stone to
navigating the world of modern cloud-native solutions. 


## Azure Arc Enabled Servers

As part of the registration of Azure Stack HCI each of the nodes in the cluster as Arc [Enabled][arcenabledservers].  This is performed at a cluster level so that any additional nodes which are added to the cluster are automatically Arc Enabled.  The benefits of this is that yiu can the use Azure to Govern, Protect, Configure and Monitor the servers.  This is perfomed by installing the [Connected Machine Agent][connectedmachineagent] onto the node so that the each of the nodes is represented as a resource within the Azure Portal, under Azure Arc. 

For this topic we will concentrate on the Monitoring aspect which is performed with the deployment of the [Azure Monitor Agent (AMA)][ama]

S