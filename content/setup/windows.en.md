---
title: Install EC2 Windows & RDP client
weight: 21
pre: "<b>2-1. </b>"
---

## Create an IAM role to apply for EC2 instance
{{% notice note %}}
The purpose of creating EC2 Windows is to configure a Jenkins server that can work with AWS CodePipeline. Therefore, you have to create the permission for the EC2 instance for connecting AWS CodePipeline first, and apply it to the EC2 instance.
{{% /notice %}} 
1. Access the [IAM role console](https://console.aws.amazon.com/iam/home). Then click on **Roles** on the left panel, and then click on **Create Role**.
![IAM Role](/images/ec2/createrole.png)

2. Then, click **AWS service** in the **Select type of trusted entity** category, click **EC2** in **Choose a use case**, and click the **Next: Permissons** button. Move on to the next.
![IAM Role](/images/ec2/createec2role.png)

3. Next, search for and select `AWSCodePipelineCustomActionAccess` in the search box, and then click the **Next: Tags** button to proceed to the next step.
![IAM Role](/images/ec2/selectpipelinerole.png)

4. In the **Add tags** section, you don't need to do anything. Click the **Next: Review** button to proceed to the next step.
![IAM Role](/images/ec2/selectpipelinerole.png)

5. Finally, in **Review**, write `ec2-windows-jenkins-role` in **Role name** and click the **Create role** button to finish creating the IAM role.




## EC2 Windows Server Launch 
{{% notice note %}}
This step is for creating an EC2 Instance. You don't have to follow this step to create it. but, this is the step to configure Jenkins server for Unity Build. So, it is recommended to create it in consideration of sufficient instance type and storage for Unity Build.
{{% /notice %}} 

1. Click the **Launch instance** button on the EC2 Dashboard.
![EC2 dashboard](/images/ec2/ec2dashboard.png)

2. On the Create EC2 page, choose your Windows AMI from **Step 1: Choose an Amazon Machine Image-AMI**. For this lab, we will select **Microsoft Windows Server 2019 Base-ami-0ff0049cd3c9a5fcb**.
{{% notice info %}}
you don't have to choose this version of the Windows Server AMI. You can choose a different Windows version AMI that Jenkins and Unity can install.
{{% /notice %}} 

3. Select Instance Type. In this case, we have chosen **c5large**.
{{% notice info %}}
It is also okay to select another type of instance (ex. t type). However, considering that it is the purpose of building a Jenkins server for Unity Build, it is recommended to select an appropriate type of Instance. If it is an EC2 Instance for this lab, the Build to be executed is an Empty Project, so it is not a heavy task, so there is no need to select an Instance Type that is too high.
{{% /notice %}} 

4. Next is **Configure Instance Details**. The parts to be set here are **Network** and **Subnet**.
   + **Network** is where you choose your VPC. Select an appropriate VPC from among the VPCs created in your console, otherwise select the **default VPC** created by default when you created your AWS account.
   + **Subnet** is where you can choose from among Subnets you have already created. If there is no subnet created, select **Create new subnet** to create a new subnet. When creating a subnet, **AZ-Availability Zone** can be selected from any AZ existing in the region. 
   + In the **IAM role**, find and select the `ec2-windows-jenkins-role` you created in the above step.

5. The rest of the settings are no meaning for this lab. So leave it and click **Next:Add Storage**.

6. **Step. 4 For Storage**, it is recommended to set **Size** of **Root Volume type** to **at least 30gb*** for Unity3d installation. Then click **Next:Add Tag**.

7. In **Next:Add Tag**, do not anything, and click **Next:Configure Security Group**.

8. **Step 6: Configure Security Group** adds 2 Inbound Rules.
   + Type: RDP, Protocol: TCP, Port Range:3389, Source: Custom 0.0.0.0/0
   + Type: Custom TCP Rule, Potocol: TCP, Port Range:8080, Source: Custom 0.0.0.0/0
![Inbound Rules](/images/ec2/ec2inbound.png)

9. After configure security group settings, click **Review and Launch**, review whether the input is correct, and click **Launch**.

10. Finally, this is the step of selecting a key pair that can access the EC2 instance. If there is a key pair already in use, select **Choose an existing key pair** and select the key pair you already have. If you need a new key pair, select **Create a new key pair**, enter the key pair name, and click **Download Key Pair** to download the file to your local PC.
{{% notice warning %}}
**The downloaded pem file** is needed for connecting to EC2 Windows instance remotely in this lab. **Please keep it.**
{{% /notice %}}

11.  EC2 Windows instance step is complete!


## Install and Connecting RDP Client
{{% notice note %}}
This process is to install the RDP client on the local PC. 2-2. Install Jenkins, 2-3. Install Unity proceeds after accessing the EC2 instance GUI environment with an RDP client.
{{% /notice %}} 

1. First, you need to check the password to access RDP. Select the Windows EC2 instance created in **EC2 Dashboard -> INSTANCES -> Instances** and click the **Connect** button.
![Connect](/images/ec2/ec2connect.png)

2. First, click **Download Remote Desktop File** in the **Connect to your instance** window to obtain an rdp file to access your EC2 instance.

3. Then click **Get Password**. Click and upload the **pem file** of your choice while creating an EC2 instance. Upload and click **Decrypt Password** to obtain a password. Save this password.

4. Install [RDP Client](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients) on the local PC.

5. If **Microsoft Remote Desktop** is properly installed, run the rdp file downloaded in step 2.
![RDP](/images/ec2/rdp.png)

6. If you enter the password saved in step 3, you can access the GUI environment of the EC2 Windows instance.

7. After connecting, when the **Network** permission window appears, click **Yes**.






---
<p align="center">
© 2021, Amazon Web Services, Inc. or its affiliates. All rights reserved.
</p>
