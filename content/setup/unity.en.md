---
title: Install Unity
weight: 22
pre: "<b>2-2. </b>"
---
{{% notice note %}}
In this course, it is a lab to proceed after connecting to Windows EC2 remotely.
{{% /notice %}}

## Allow IE download permission
Initial Windows EC2 instance has IE Enhanced Security Configuration enabled, so files cannot be downloaded through external internet.
Therefore, refer to the **Solution** in [Downloader Troubleshooting Document](https://aws.amazon.com/en/premiumsupport/knowledge-center/ec2-windows-file-download-ie/?nc1=h_ls). Follow along and change the IE settings to enable download.
![IE allow download](/images/ec2/allowdownload.png)

## Install Unity
1. Connect to a Windows EC2 instance remotely, access the Unity Download link from an Internet browser, and [Download](https://unity3d.com/get-unity/download) **Unity Hub**.
![Unity Download](/images/ec2/unitydownload.png)

2. No special configuration is required to install Unity. Complete the installation with the default settings.

3. When the installation is complete, launch Unity Hub and click **Cogwheel-Preferences** on the top right. Then click **License Management**, click **Manage License** at the bottom, and click **Login** in succession to proceed with Log-in. Click **ACTIVATE NEW LICENSE**.
{{% notice info %}}
A Unity account is required to obtain a Unity License. If you do not have an account, you can create a new account through this process.
{{% /notice %}}

4. Click on **Unity Personal** in **License Agreement**. Then select **I don't use Unity in a professional capacity** and click **DONE**.
![Unity License](/images/ec2/unitygetlicense.png)
![Unity License](/images/ec2/unitylicense.png)
---
{{% notice info %}}
If you already have a license, you can use your own license instead of a new personal license.
{{% /notice %}}

5. When the license is activated, click **<- Preferences** on the top left and click **Installs**.

6. Click the **ADD** button to select the version in **Recommended Release** and click **NEXT**.
![Add Unity Version](/images/ec2/unityversion.png)

7. In **Add modules to your install** Step, select **Android Build Support** and click **NEXT**.
![Add Unity Version](/images/ec2/unityinstall.png)
![Install Unity](/images/ec2/unityinstall2.png)
---

{{% notice warning %}}
If installation is not possible due to insufficient capacity, you can expand the EBS volume by referring to [here](https://aws.amazon.com/en/premiumsupport/knowledge-center/expand-ebs-root-volume-windows/).
{{% /notice %}}

8. When all installation is complete, you are ready to create a Jenkins Job.





---
<p align="center">
© 2021, Amazon Web Services, Inc. or its affiliates. All rights reserved.
</p>
