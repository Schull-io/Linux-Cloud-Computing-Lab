# Lab 2: Manage Linux VMs with the AWS CLI


 ### Create virtual machine

    > my code input:
    ```
    aws ec2 run-instances \
        --image-id ami-0c4f7023847b90238 \
        --instance-type t2.micro \
        --key-name poly4key
        --security-group-ids sg-05d92cf7903c4c896
    ```
 ### Connect to VM
    ```
    I used the amazon EC2 instance connect to connect to my VM
    ```
 ### Understand VM images
    * I Launched an instance and select a Community AMI configure the instance
    * I connected the instance with SSH

 ### VM power states
    #### stop instance
    > my code input
    ```
    aws ec2 stop-instances --instance-ids i-5203422c
    ```
    #### terminate instance
    > my code input
    ```
    aws ec2 terminate-instances --instance-ids i-5203422c
    ```



Notes:
Quickstart: Create a Linux VM

https://aws.amazon.com/getting-started/launch-a-virtual-machine-B-0/
Using a custom Amazon machine image (AMI)

https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.customenv.html
Quickstart: Restart VM via CLI

https://docs.aws.amazon.com/cli/latest/reference/ec2/reboot-instances.html
Quickstart for AWS CloudShell

https://docs.aws.amazon.com/cloudshell/latest/userguide/working-with-cloudshell.html