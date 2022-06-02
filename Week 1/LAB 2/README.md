# Lab 2: Manage Linux VMs with the Azure CLI

Task: 

1. Create resource group
    > Here is the input code for creating my resource group:
    ```
    az group create --location australiaeast --n MyResourceGroupVM
    ```
    > Here is the output code for creating a resource group:
    ```
    {
    "id": "/subscriptions/b5549425-9749-48f8-8db1-e22c7d47472d/resourceGroups/myResourceGroupVM",
    "location": "australiaeast",
    "managedBy": null,
    "name": "myResourceGroupVM",
    "properties": {
        "provisioningState": "Succeeded"
    },
    "tags": null,
    "type": "Microsoft.Resources/resourceGroups"
    }
    ```
2. Create virtual machine

    > Code input:
    ```
    az vm create
    --resource-group myResourceGroupVM
    --name myVM
    --image UbuntuLTS
    --admin-username poly4
    --generate-ssh-keys
    --size Standard_B1ls
    ```

    > Here is the output code for creating my virtual machine:
    ```
    {
    "fqdns": "",
    "id": "/subscriptions/b5549425-9749-48f8-8db1-e22c7d47472d/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
    "location": "australiaeast",
    "macAddress": "00-0D-3A-52-F7-64",
    "powerState": "VM running",
    "privateIpAddress": "10.0.0.4",
    "publicIpAddress": "52.191.113.133",
    "resourceGroup": "myResourceGroupVM",
    "zones": ""
    }
    ```
3. Connect to VM

    > Code input
    ```
    ssh poly4@52.191.113.133
    ```

4. Understand VM images

    > Read the [Docs](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-vm)

    #### Create a VM with a specific VM Image
    > Code input:
    ```
    az vm create
    --resource-group myResourceGroupVM
    --name poly4VM
    --image OpenLogic:CentOS:7.5:latest
    --generate-ssh-keys
    --size Standard_B1ls
    ```

    > Here is the output code:
    ```
    {
    "fqdns": "",
    "id": "/subscriptions/b5549425-9749-48f8-8db1-e22c7d47472d/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/poly4VM",
    "location": "australiaeast",
    "macAddress": "00-22-48-28-FB-C3",
    "powerState": "VM running",
    "privateIpAddress": "10.0.0.5",
    "publicIpAddress": "52.170.102.44",
    "resourceGroup": "myResourceGroupVM",
    "zones": ""
    }
    ```

5. Understand VM sizes

    > Read the [Docs](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-vm)
    #### Create a VM with a specific VM Size
    > Code input:
    ```
    az vm create
    --resource-group myResourceGroupVM
    --name myVM3
    --image UbuntuLTS
    --size Standard_B1s
    --generate-ssh-keys
    ```

    > Here is the output code:
    ```
    {
    "fqdns": "",
    "id": "/subscriptions/b5549425-9749-48f8-8db1-e22c7d47472d/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM3",
    "location": "australiaeast",
    "macAddress": "00-0D-3A-14-21-08",
    "powerState": "VM running",
    "privateIpAddress": "10.0.0.4",
    "publicIpAddress": "13.82.83.216",
    "resourceGroup": "myResourceGroupVM",
    "zones": ""
    }
    ```

    #### Resize a VM
    ##### show the size of VM
    > Code input:
    ```
    az vm show --resource-group myResourceGroupVM --name myVM3 --query hardwareProfile.vmSize
    ```

    > Here is the output:
    ```
    "Standard_B1s"
    ``` 

    ##### change size of VM
    
    > Code input:
    ```
    az vm resize --resource-group myResourceGroupVM --name myVM3 --size "Standard_B1ls"
    ```

    > Here is a partial output:
    ```
    {
    "additionalCapabilities": null,
    "applicationProfile": null,
    "availabilitySet": null,
    "billingProfile": null,
    "capacityReservation": null,
    "diagnosticsProfile": null,
    "evictionPolicy": null,
    "extendedLocation": null,
    "extensionsTimeBudget": null,
    "hardwareProfile": {
        "vmSize": "Standard_B1ls",
        "vmSizeProperties": null
    },
    "tags": {},
    "type": "Microsoft.Compute/virtualMachines",
    "userData": null,
    "virtualMachineScaleSet": null,
    "vmId": "ab10b743-bffc-426d-afc6-259fd69282aa",
    "zones": null
    }
    ```
6. VM power states
    #### Current powerstate  of my VM:

    > Code input
    ```
    az vm get-instance-view
    --name poly4VM
    --resource-group myResourceGroupVM
    --query instanceView.statuses[1] --output table
    ```
    > output
    ```
    Code                Level    DisplayStatus
    ------------------  -------  ---------------
    PowerState/running  Info     VM running
    ```
7. Management tasks
    #### To get IP address:
    > Code input
    ```
    az vm list-ip-addresses --resource-group myResourceGroupVM --name poly4VM --output table
    ```
    > output
    ```
    PowerState/running  Info     VM running
    poly4@Azure:~$ az vm list-ip-addresses --resource-group myResourceGroupVM --name poly4VM --output table
    VirtualMachine    PublicIPAddresses    PrivateIPAddresses
    ----------------  -------------------  --------------------
    poly4VM           52.170.102.44        10.0.0.5
    ```

Notes:
Quickstart: Create a Linux VM

https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-vm
Quickstart for Bash in Azure Cloud Shell

https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart