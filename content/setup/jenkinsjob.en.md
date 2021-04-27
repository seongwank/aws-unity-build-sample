---
title: Creating Unity Build Job
weight: 24
pre: "<b>2-4. </b>"
---

## Jenkins Install plug-ins & Configuration

1. Open Jenkins to do the plugin and settings.
{{% notice info %}}
When connecting and configuring remotely using RDP, access **localhost:8080**. To configure Jenkins on a local PC, access **Your EC2 public DNS adderess:8080**.
{{% /notice %}}
2. If you have connected to Jenkins, click **Jenkins Management-Manage Jenkins**, then click **Manage Plugins** and click **Installable-Available** tab.
![Install CodePipeline](/images/ec2/awspipeline.png)

3. Search for **AWS CodePipeline** and click the **left check box**. Then search for **Unity3d plugin** and click the **left check box**. And click **Install without restart** at the bottom to complete installation.
![Install CodePipeline](/images/ec2/unityplugin.png)

4. When this installation is complete, click **Jenkins Management** on the first screen again and click **Global Tool Configuration**.

5. Click on **Unity3d installations** under **Unity3d**. Click **Add Unity3d** and write `Unity 2019.xx.xxf(your version)` in **Name**. And write the path of Unity installed in **Installation directory**.

{{% notice info %}}
If you have followed this process in the same way as in this lab, Unity Directory Path is `C:\Program Files\Unity\Hub\Editor\20xx.x.xxfx`. If not, write Drectory Path where you installed Unity.
{{% /notice %}}




## Creating Jenkins Unity Build Job

1. On the first screen of Jenkins, click on **New Item-New item** on the left frame.

2. Write `unity-android-build` in **Enter an item name** field, select **Freestyle proeject** at the bottom, and click **OK**.

3. On the job creation screen, select **AWS CodePipeline** from **Source Code Management** tab.

4. Select your region from **AWS Region**. In this lab, we chose Asia Pacific(Seoul) ap-northeast-2**. And in **Category**, select `Build`. Finally, for **Provider**, enter `android-build-provider`. Otherwise, you can leave it as it is without anything.
![CodePipeline setting](/images/ec2/awscodepipeline.png)
{{% notice note %}}
**Provider** is an essential variable for CodePipeline's Build setting.
{{% /notice %}}

5. In **Build Triggers**, select **Poll SCM** and enter `* * * * *`.
![Build Triggers](/images/ec2/pollscm.png)

6. Select **Add build step** from **Build**, then click **Invoke Unity3d Editor**.

7. In **Unity3d installation name**, select **Unity3d Editor** you wrote in **Global Configuration**.

8. Write `-quit -batchmode -executeMethod Builder.PerformAndroidBuild -logFile "C:\Users\Administrator\Documents\android_build.log"` on **Editor command line arguments**

9. Once again, select **Add build step** and click **Execute Windows batch command**.

10. In **Command** field, enter `mkdir apk` in first line and `move android_build_lab.apk apk/android_build_lab.apk` in second line.
![Jenkins Job Build Step](/images/ec2/jenkinsjobbuildstep.png)

1.  Finally, in **Post-build Actions-Post-build Actions** item, click **Add post-build action**, and then click **AWS CodePipeline Publisher**. And write `/apk/` in **Location** field. Write `BuildArtifact` in **Artifact Name** field.
![Jenkins Post Build Step](/images/ec2/jenkinspostbuild.png)
{{% notice note %}}
**Artifact Name** is an essential variable in CodePipeline's Build setting.
{{% /notice %}}

1.  Click the **Save** button at the bottom to complete Jenkins Job creation.




---
<p align="center">
© 2021, Amazon Web Services, Inc. or its affiliates. All rights reserved.
</p>
