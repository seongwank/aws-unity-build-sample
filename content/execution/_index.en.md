---
title: Running AWS CodePipeline
weight: 40
pre: "<b>4. </b>"
---

{{% notice note %}}
In this step, after completing the creation of AWS CodePipeline, we will take a closer look at the steps in AWS CodePipline.
{{% /notice %}}

## Test AWS CodePipeline

1. When you finish creating the CodePipeline, the pipeline is automatically executed, and you can see that the Source stage changes to In progress.
![codepipeline](/images/execution/initialexecution.png)
{{% notice info %}}
If you want to run the pipeline yourself, press **Release change** to run the pipeline. Also, if you want to run CodePipeline automatically, you can find information in [chnage dection methods](https://docs.aws.amazon.com/codepipeline/latest/userguide/pipelines-about-starting.html#change-detection-methods) and   [CodePipeline notification rule](https://docs.aws.amazon.com/dtconsole/latest/userguide/getting-started-pipeline.html)
{{% /notice %}}

2. When the source phase completes successfully, the Build phase will be in progress. To check Jenkins job status, click **Custom android-build-provider** to switch to the Jenkins Job page.
![codepipeline](/images/execution/jenkins.png)

3. When the Build and Deploy steps are completed, all phases are marked as **Succeeded** as shown in the picture below.
![codepipeline](/images/execution/pipeline.png)

4. To check the artifacts deployed in S3, click **Amazon S3** in the Deploy step to access the S3 bucket and check the artifacts.
![codepipeline](/images/execution/s3.png)

<!--앞으로 해야할일
AMI로 설치과정을 간단하게 만들기,
Mac instance가 나오면 ios빌드까지 추가하기
test 환경으로 자동으로 artifacts가 입력되고 알림보내기(aws device farm)
-->
<p align="center">
© 2021, Amazon Web Services, Inc. or its affiliates. All rights reserved.
</p>


