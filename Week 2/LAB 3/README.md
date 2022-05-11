# Lab 3: Manage Packages and Services on a Linux VM (Azure or AWS)


1. Create a Linux VM
    > my code input:
    ```
    aws ec2 run-instances \
        --image-id ami-0c4f7023847b90238 \
        --instance-type t2.micro \
        --key-name poly4key
        --security-group-ids sg-05d92cf7903c4c896
    ```
    * Then I connect to the VM using the EC2 instance connect 
2. Install the Apache Web Server
    >my code input to install:
    ```
    sudo apt update -y
    sudo apt install -y apache2
    ```
3. Start the service status via command line
    >my code input to start server
    ```
    sudo service apache2 start
    ```
4. Investigate the service status via command line
    >my code input to investigate the server
    ```
    sudo service apache2 status
    ```
5. Stop the service
    >my code input to stop server
    ```
    sudo service apache2 stop
    ```

Challenge: Create a boostrapping script that will install and start this service on new EC2 VMs
    
    * Server installation and starting command
    ```
    sudo yum update -y
    sudo yum install -y httpd
    sudo service start httpd
    ```
    * Add the above script in the `user data` box in the `advance details` section of the instance creation

    
Notes:

Install and Configure Apache (Ubuntu)

https://ubuntu.com/tutorials/install-and-configure-apache#1-overview
How to install Apache on RHEL 8 / CentOS 8 Linux

https://linuxconfig.org/installing-apache-on-linux-redhat-8
How to use cloud-init to customize a Linux virtual machine in Azure on first boot

https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-automate-vm-deployment
Create bootstrap actions to install additional software

https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-bootstrap.html