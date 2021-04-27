---
title: Install Jenkins
weight: 23
pre: "<b>2-3. </b>"
---

{{% notice note %}}
In this course, it is a lab to proceed after connecting to Windows EC2 remotely.
{{% /notice %}}

## Install JDK
1. If you have enabled download permission, you need to install Java JDK first to install Jenkins. [Download](https://jdk.java.net/java-se-ri/11) of JDK 11 of Windows x64 product.
{{% notice info %}}
In this lab, we will use JDK 11. Currently (February 2021) Jenkins can be installed using [JDK 8, JDK 11 version](https://www.jenkins.io/doc/administration/requirements/java/). Since it is only used for Jenkins installation, there is no need to worry about it. because it doesn't match the JDK version you are actually using. You can also install it with openJDK as well as oracle JDK.
{{% /notice %}}

2. In File Explorer, copy **jdk-11** in openjdk-11+xx_windows-x64_bin folder of Download folder to subfolder of **C:\Program Files\java**.
![JDK 11 Download](/images/ec2/jdkcopy.png)




## Install Jenkins
1. When the JDK is installed, you can install Jenkins. First, download **Windows** version of Jenkins (https://www.jenkins.io/download/).
![Jenkins Download](/images/ec2/jenkinsdownload.png)
{{% notice info %}}
In this lab, we used the 2.263.3 LTS version. This version is not the required version to do this lab. You can also download other 2.xxx.x versions for this lab.
{{% /notice %}}

2. After downloading Jenkins, run **jenkins** in the Download folder in File Explorer to install.
{{% notice info %}}
During installation, in the **Service Logon Credentials** Step, select **Run service as local or domain user**. And Account is `Administrator` and Password is **Password read to access RDP client from EC2 Console**.
{{% /notice %}}
![Jenkins installation failure screen](/images/ec2/jenkinsprivilege.png)
   #### If the installation fails as shown in the picture above, you can solve the problem by following the steps below.
   + Click Search (magnifying glass) in the lower left corner of Windows, search for **Administrative Tools** and run **Local Security Policy**.
   + Click **Local Policies**, then **User Rights Assignment**.
   + Right-click the **Log on as a service** item in the right panel and select **properties**.
   + Click **Add User or Group**, write `administrator` in **Enter the object names to select**, click **Check Names**, and click **OK**.
   ![Allow port](/images/ec2/allowprivilege.png)

3. In the window to select the Java home directory during installation, specify `C:\Program Files\java\jdk-11` copied above.
![Jenkins admin](/images/ec2/choosejdkpath.png)

4. When Jenkins installation is complete, click the Start button in the completion window to run Jenkins.

5. Open an Internet browser on a Windows EC2 instance accessed remotely and access **localhost:8080**. In **Unlock Jenkins**, open the **initialAdminPassword** file in Notepad and write Administrator password. In **Customize Jenkins**, select **Install suggested plugins**. Complete all settings and click **Save and Finish** to complete the installation.
![Jenkins admin](/images/ec2/jenkinsadmin.png)

6. If you proceed to step 4, the Jenkins installation is all complete. However, in order for Local PC and AWS CodePipeline to access, you need to take action to open a port of Windows and allow access.
   - Click Search (magnifying glass) in the lower left corner of Windows.
   - Write `Windows Defender Firewall` and click **Windows Firewall control panel**.
   - Select **Advanced settings** on the left frame.
   - Click on **Inbound Rules** in the left frame. Then click on **New Rule** on the right frame.
   - Select **Port** and click **Next**.
   - Select **TCP**, click **Specific local ports**, enter `8080`, and click **Next**.
   - Select **Allow the connection** and click **Next**.
   - Select **Public** and click **Next**.
   - Write `Jenkins port` in **Name** and click **Finish**.
![Allow port](/images/ec2/allowport.png)

7. In order to check whether the port is properly connected, test using the public DNS of the Windows EC2 instance.
Public DNS can be found in **EC2 dashboard -> Running Instances -> Windows EC2 selection -> Public DNS(IPv4)** in AWS console.
![Public DNS](/images/ec2/publicdns.png)

{{% notice warning %}}
If it is not possible to access jenkins through public DNS, you need to check whether the system such as VPN running on the local PC is blocking the 8080 port.
{{% /notice %}}




---
<p align="center">
© 2021, Amazon Web Services, Inc. or its affiliates. All rights reserved.
</p>
