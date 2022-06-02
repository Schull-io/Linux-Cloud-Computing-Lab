# Lab 3: Manage Azure disks with the Azure CLI

Task:

1. Default Azure disks
    > Read the [Docs](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-disks)

2. Azure data disks
    > Read the [Docs](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-disks)

3. VM disk types
    > Read the [Docs](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-disks)

4. Launch Azure Cloud Shell
    ```
    launch cloud shell from the navigation pan on azure portal
    ```
5. Create and attach disks
    #### Create Resource Group
    > Here is the input code for creating a resource group:
    ```
    az group create --location australiaeast --name MyResourcegroupdisk
    ```
    > Here is the output code for creating a resource group:
    ```
    {
    "id": "/subscriptions/b5549425-9749-48f8-8db1-e22c7d47472d/resourceGroups/MyResourcegroupdisk",
    "location": "australiaeast",
    "managedBy": null,
    "name": "MyResourcegroupdisk",
    "properties": {
        "provisioningState": "Succeeded"
    },
    "tags": null,
    "type": "Microsoft.Resources/resourceGroups"
    }
    ```
    #### Create Resource Group
    The following example creates a VM with 2 additional 5gb datadisks
    > Code input:
    ```
    az vm create
    --resource-group myResourceGroupDisk
    --name poly4VM
    --image UbuntuLTS
    --size Standard_B1ls
    --admin-username poly4
    --generate-ssh-keys
    --data-disk-sizes-gb 5 5
    ```

    > Here is the output code for creating my virtual machine:
    ```
    {
    "fqdns": "",
    "id": "/subscriptions/b5549425-9749-48f8-8db1-e22c7d47472d/resourceGroups/myResourceGroupDisk/providers/Microsoft.Compute/virtualMachines/poly4VM",
    "location": "australiaeast",
    "macAddress": "00-0D-3A-17-7E-BB",
    "powerState": "VM running",
    "privateIpAddress": "10.0.0.4",
    "publicIpAddress": "20.119.51.160",
    "resourceGroup": "myResourceGroupDisk",
    "zones": ""
    }
    ```
6. Prepare data disks

* Create an SSH connection with the virtual machine
    `poly4@20.119.51.160`
    * Partition the disk with `parted`
    ```
    sudo parted /dev/sdc --script mklabel gpt mkpart xfspart xfs 0% 100%
    ```
    * Write a file system to the partition by using the `mkfs` command. Use `partprobe` to make the OS aware of the change.
    ```
    sudo mkfs.xfs /dev/sdc1
    sudo partprobe /dev/sdc1
    ```

    * Mount the new disk so that it is accessible in the operating system.
    ```
    sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
    ```
    * The disk can now be accessed through the `/datadrive `mountpoint, which can be verified by running the `df -h` command.
    ```
    df -h | grep -i "sd"
    ```
    > Output
    ```
    /dev/sdb1        29G  1.4G   28G   5% /
    /dev/sdb15      105M  4.4M  100M   5% /boot/efi
    /dev/sda1        14G   41M   13G   1% /mnt
    /dev/sdc1       128G  163M  128G   1% /datadrive
    ```
    * To ensure that the drive is remounted after a reboot, it must be added to the `/etc/fstab` file. To do so, get the UUID of the disk with the `blkid` utility.
    ```
    sudo -i blkid
    ```
    > UUID
    ```
    UUID="ddb9676f-9912-41e4-a9a8-1eba765ca761" TYPE="xfs"
    ```
    * Open the `/etc/fstab` file in a text editor as follows:
    ```
    sudo nano /etc/fstab
    ```
    > input int the `/etc/fstab` file
    ```
    UUID=ddb9676f-9912-41e4-a9a8-1eba765ca761 /datadrive  xfs defaults,nofail   1  2  3
    ```
    * Close connection
    ```
    exit
    ```
7. Take a disk snapshot
    Before you create a snapshot, you need the ID or name of the disk.
    > Code input
    ```
    osdiskid=$(az vm show -g myResourceGroupDisk -n poly4VM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
    ```
    #### snapshot
    > input 
    az snapshot create \
    --resource-group myResourceGroupDisk \
    --source "$osdiskid" \
    --name osDisk-backup

    #### create disk from snapshot
    az disk create \
   --resource-group myResourceGroupDisk \
   --name mySnapshotDisk \
   --source osDisk-backup


Notes:
Quickstart: Manage Azure disks

https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-disks
Quickstart for Bash in Azure Cloud Shell

https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart