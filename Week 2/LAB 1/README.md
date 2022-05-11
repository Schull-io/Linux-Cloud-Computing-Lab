# Lab 1: Create a Linux virtual machine with the AWS CLI


1. Launch AWS Cloud Shell

    ```
    I launched cloud shell from the navigation pan on aws portal
    ```

2. Create virtual machine

    > my code input:
    ```
    aws ec2 run-instances \
        --image-id ami-0c4f7023847b90238 \
        --instance-type t2.micro \
        --key-name poly4key
        --security-group-ids sg-05d92cf7903c4c896
    ```
3. Open port 80 for web traffic
    ```
    The security group I added to the ec2 during creation allow https access
    ```
4. Connect to virtual machine
     ```
    I used the amazon EC2 instance connect to connect to my VM
    ```
5. Install web server   
    >my code input to install:
    ```
    sudo apt update -y
    sudo apt install -y apache2
    ```
    * Start server

    >my code input to start server
    ```
    sudo systemctl start apache2
```
6. View the web server in action
    > Here is a screenshot of the web server in action:
    ![apache web server](images/apache.png)


Notes:
Quickstart: Create a Linux VM

https://aws.amazon.com/getting-started/launch-a-virtual-machine-B-0/
Quickstart for AWS CloudShell

https://docs.aws.amazon.com/cloudshell/latest/userguide/working-with-cloudshell.html