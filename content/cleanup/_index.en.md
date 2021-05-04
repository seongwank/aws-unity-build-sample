---
title: Clean Up
weight: 50
pre: "<b>5. </b>"
---

{{% notice note %}}
This step is the process of deleting all resources after the lab is over.
{{% /notice %}}

## EC2 제거
1. 먼저 Jenkins가 설치된 EC2 Instance를 확인하기 위하여 EC2 console 화면으로 진입하여 리스트에서 Jenkins EC2 인스턴스를 클릭하고, Security 탭을 클릭하여 Security Group id를 확인합니다. 
![EC2 Security](/images/cleanup/ec2_security.png)
2. EC2를 아래의 사진과 같이 종료합니다.
![Terminate EC2](/images/cleanup/ec2_terminate.png)
3. 1.에서 확인한 Security Group Id를 왼쪽 탭의 **Network & Security -> Security Groups**에서 찾아 삭제합니다.
![Delete Security Group](/images/cleanup/ec2_sg_delete.png)
4. 혹시 Jenkins EC2 인스턴스를 생성 할 때, 아래 사진과 같이 delete on termination을 활성화 하지 않았다면 EBS(Elastic Block Storage)도 함께 삭제해줘야 합니다.
![Delete EBS](/images/cleanup/ec2_terminate_dbs.png)


## AWS CodePipeline 제거
AWS CodePipeline 콘솔에서 `unity-build-pipeline`을 찾아 클릭합니다. 그리고 Edit 버튼을 클릭하고, 다음 화면에서 Delete를 클릭하여 삭제를 완료합니다.
![Edit CodePipeline](/images/cleanup/code_pipeline_edit.png)
![Delete CodePipeline](/images/cleanup/code_pipeline_delete.png)

## S3 bucket 삭제
S3 콘솔화면에서 `unity-build-output` 버킷을 삭제합니다.
{{% notice note %}}
아래 사진과 같이 버킷내 파일을 먼저 삭제해야 버킷을 삭제할 수 있습니다.
{{% /notice %}}
![Delete S3 Bucket](/images/cleanup/s3_bucket_delete.png)

## IAM role 삭제
실습에서 사용된 IAM role은 총 2개입니다. EC2 인스턴스에 사용한 IAM role, CodePipeline에서 자동생성된 IAM role 입니다. `ec2-windows-jenkins-role`, `AWSCodePipelineServiceRole`을 검색하여 삭제합니다. 
{{% notice note %}}
CodePipeline IAM role은 여러분의 리전과 Pipeline 이름을 참고하여 자동 생성됩니다.
{{% /notice %}}
![Delete IAM role](/images/cleanup/iam_delete.png)
![Delete IAM role](/images/cleanup/iam_delete_2.png)

---
<p align="center">
© 2021 Amazon Web Services, Inc. 또는 자회사, All rights reserved.
</p>
