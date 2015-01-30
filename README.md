# VMWare-DRP
A DIY VMWare DRP using home-made command-line tools instead of $$$ ones.   
   
*This is a W.I.P*   
   
Assuming:   
* You've a few hundred VM to restore
* You don't want to invest in SRM (Site Recovery Manager)
* You've a fail-over SAN with LUN replica of your master SAN
   
The big picture is to restart some of your VM on your DR site based on your LUN replica.   
In order to do it, you'll make use of the following tools:   
* [vmdatastore](https://github.com/sebbrochet/vmdatastore): This command-line tool lets you add datastores to your ESX hosts   
* [vminventory](https://github.com/sebbrochet/vminventory): vCenter inventory update from .vmx files tool   
* [vmmetadata](https://github.com/sebbrochet/vmmetadata): vCenter metadata (custom fields) export/import tool   
* [vmlauncher](https://github.com/sebbrochet/vmlauncher): Command-line client to send start/stop commands to a set of VMs in a VMWare vCenter host   
   
*vmdatastore* is not really required if you configure your LUN replica to be auto-mounted when they are presented to your ESX servers.   
See this [VMWARE KB](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1011387) for some details.   
   
*vminventory* is used to add to the inventory all the VM stored in your LUN replica in one go.   
   
*vmmetadata* is used to export/backup your metadata from your production site to your DR site.   
Metadata are used by *vmlauncher* to describe the starting order and dependencies of the VM   
   
*vmlauncher* controls the starting of the VM in the right order.