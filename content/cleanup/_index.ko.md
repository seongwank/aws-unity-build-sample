---
title: Clean Up
weight: 50
pre: "<b>5. </b>"
---

{{% notice note %}}
This step is the process of deleting all resources after the lab is over.
{{% /notice %}}

## Delete EC2 instance
1. First, enter the EC2 console window to check the EC2 Instance where Jenkins is installed, then click the Jenkins EC2 instance from EC2 list, and click Security tab to check the Security Group ID.
![EC2 Security](/images/cleanup/ec2_security.png)
2. Delete EC2 as shown in the picture below.
![Terminate EC2](/images/cleanup/ec2_terminate.png)
3. Search for Security Group Id in **Network & Security -> Security Groups** on the left tab, and delete it.
![Delete Security Group](/images/cleanup/ec2_sg_delete.png)
When creating a Jenkins EC2 instance, if you have not enabled delete on termination as shown in the picture below, you have to also delete EBS (Elastic Block Storage).
![Delete EBS](/images/cleanup/ec2_terminate_dbs.png)


## Delete AWS CodePipeline
Find and click on `unity-build-pipeline` in the AWS CodePipeline console. Then click the Edit button and click Delete button on the next window.
![Edit CodePipeline](/images/cleanup/code_pipeline_edit.png)
![Delete CodePipeline](/images/cleanup/code_pipeline_delete.png)

## Delete S3 bucket
Delete the `unity-build-output` bucket from the S3 console window.
{{% notice note %}}
As shown in the picture below, you have to delete all files in the bucket before deleting the bucket.
{{% /notice %}}
![Delete S3 Bucket](/images/cleanup/s3_bucket_delete.png)

## Delete IAM role
There are a total of 2 IAM roles used in the lab. IAM role used for EC2 instance, IAM role automatically created in CodePipeline. Search for `ec2-windows-jenkins-role` and `AWSCodePipelineServiceRole` and delete them.
{{% notice note %}}
The CodePipeline IAM role is automatically created based on your region and pipeline name.
{{% /notice %}}
![Delete IAM role](/images/cleanup/iam_delete.png)
![Delete IAM role](/images/cleanup/iam_delete_2.png)

---
<p align="center">
© 2021, Amazon Web Services, Inc. or its affiliates. All rights reserved.
</p>
