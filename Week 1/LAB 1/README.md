# Lab 1: Create a Linux virtual machine with the Azure CLI

1. Launch Azure Cloud Shell

```
launch cloud shell from the navigation pan on azure portal
```

2. Create a resource group

> Here is the input code for a creating resource group:
```
az group create --location australiaeast --name MyResourcegroup
```
> Here is the output code for creating a resource group:

```
    {
    "id": "/subscriptions/b5549425-9749-48f8-8db1-e22c7d47472d/resourceGroups/myResourceGroup",
    "location": "australiaeast",
    "managedBy": null,
    "name": "myResourceGroup",
    "properties": {
        "provisioningState": "Succeeded"
    },
    "tags": null,
    "type": "Microsoft.Resources/resourceGroups"
    }
```

3. Create virtual machine

Code input:
```
az vm create
--resource-group myResourceGroup
--name myVM
--image UbuntuLTS
--admin-username poly4 \
--generate-ssh-keys
--size Standard_B1ls
```

> Here is the output code for creating my virtual machine:
```
{
  "fqdns": "",
  "id": "/subscriptions/b5549425-9749-48f8-8db1-e22c7d47472d/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "australiaeast",
  "macAddress": "00-0D-3A-52-F7-64",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.191.113.133",
  "resourceGroup": "myResourceGroup",
  "zones": ""
}
```
4. Open port 80 for web traffic

> Code input:
```
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

5. Connect to virtual machine
> Code input
```
ssh poly4@52.191.113.133
```

6. Install web server

> Code input
```
sudo apt-get -y update
sudo apt-get -y install apache2
```

7. View the web server in action
> Here is a screenshot of the web server in action:
![apache web server](images/apache.png)





Notes:
Quickstart: Create a Linux VM

<https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-cli>

Quickstart for Bash in Azure Cloud Shell

<https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart>
