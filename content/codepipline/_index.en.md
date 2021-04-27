---
title: Building AWS CodePipline 
weight: 30
pre: "<b>3. </b>"
---

{{% notice note %}}
In this step, we will create AWS Codepipline and integrate it with Jenkins. All work is done in the AWS console.
{{% /notice %}}

## fork GitHub Repository (empty unity project)
First, before getting started with AWS CodePipeline, it needs to create a Repository on GitHub for use in this lab. There is already an Empty unity project ready for this lab. Click [here](https://github.com/seongwank/empty_unity_sample) to open the Github repository browser. And fork this Repository to your Account. You can connect to AWS CodePipeline using your Git Account simply by clicking the **Fork button** on the Github page as shown in the picture below.
![Github](/images/codepipeline/githubfork.png)



## Creating AWS CodePipeline

1. Click the **Create new pipeline** button on the **AWS CodePipeline Console**.
![CodePipeline Console](/images/codepipeline/pipelineconsole.png)

2. Write `unity-build-pipeline` in the **pipeline name** of the **pipeline settings** section. For **Service role**, select **New Service role** and leave the rest of the settings as they are.
![CodePipeline Console](/images/codepipeline/codepipelinesetting.png)

3. For **Source provider** in **Add source stage**, choose **GitHub (Version 2)**. Click **Connect to GitHub** in Connection.
![CodePipeline Console](/images/codepipeline/connectgithub.png)

4. You can freely create a name in the Conenction name of **Create GitHub App connection**. In this case, I will simply write `my GitHub`. After filling out, click **Connect to GitHub**. Click on **Authorize AWS Connector for GitHub** in the new window.
![CodePipeline Console](/images/codepipeline/mygithub.png)

5. When a new window shown below picture, click Install a new app.
![CodePipeline Console](/images/codepipeline/githubinstallnew.png)

6. When the window shown below picture, you can select **All repositories**, but you can select only specific Repositories you want to connect. If you want to connect only specific Repositories, select **Only select repositories**, and select **empty_unity_sample** forked in Upper Step.
![CodePipeline Console](/images/codepipeline/selectrepo.png)

7. In **Repository name**, select the Github Repository forked in the previous step(**"your github account"/empty_unity_sample**). And select **main** for **Branch name**. For **Change detection options**, disables **Start the pipeline on source code change**. For **Output arthifact format**, select **CodePipeline default** and click **Next**.
![CodePipeline Console](/images/codepipeline/setrepo.png)

8. In **Build provider**, choose **Add Jenkins**. For **Provider name**, write `JenkinsProvider`. write the **Server URL** using the Windows EC2 public DNS address in Step 2.3 likes **http://your-ec2-public-dns:8080/job/**. For **Project name**, write `unity-android-build`. Then click **Next**.
![CodePipeline Console](/images/codepipeline/buildstage.png)
{{% notice info %}}
Provider name is the Provider name you created in the AWS Codepipeline step of the Jenkins Job.
And the Project name is Jenkins Job name.
{{% /notice %}}

9. In **Add deploy stage**, select **Amazon S3** from **Deploy provider**. **Region** is your region (in this lab proceed based on **ap-northeast-2**). And select Bucket to save output artifacts. If there is no bucket, you can simply create it in S3 Console as shown below picture.
![CodePipeline Console](/images/codepipeline/createbucket.png)

10. In **Deployment path**, write `android-output`. Then, check **Extract file before deploy** checkbox and click **NEXT**.
![CodePipeline Console](/images/codepipeline/deploystage.png)

11. Review it has been created properly, and if there is no problem, click **Create Pipeline** to create a pipeline.

---
<p align="center">
© 2021, Amazon Web Services, Inc. or its affiliates. All rights reserved.
</p>