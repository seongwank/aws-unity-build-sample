---
title: AWS CodePipline 만들기 
weight: 40
pre: "<b>3. </b>"
---

**본 Step에서는 AWS Codepipline을 만들고 Jenkins와 연동하는 작업이 진행됩니다. 모든 작업은 AWS console에서 진행됩니다.** <br/><br/>
## CodeCommit 세팅하기

## AWS CodePipeline 생성하기

1. **AWS CodePipeline Console**의 **Create new pipeline**버튼을 클릭합니다.
![CodePipeline Console]("/images/codepipeline/pipelineconsole.png")

2. **Choose pipeline settings** 항목의 **pipeline name**에 **unity-build-pipeline**을 입력합니다. **Service role**은 **New Service role**을 선택하고 나머지 설정은 그대로 둡니다.
(이미지)

3. **Add source stage**의 **Source provider**에서는 **AWS CodeCommit**을 선택합니다. **Repository name**에서는 전 step에서 만든 CodeCommit Repository name을 입력합니다(**unity-build**). **Branch name**은 **master**를 선택합니다. **Change detection options**에서는 **AWS CodePipeline**을 선택합니다.
![CodePipeline Console]("/images/codepipeline/sourcestage.png")

4. **Build provider**에서 **Add Jenkins**를 선택합니다. **Provider name**은 **Jenkins_Provider**을 입력합니다. **Server URL**에는 Step 2.3에서 테스트해본 Windows EC2 public DNS의 주소를 활용하여 입력합니다. **ex) http://your-public-dns:8080/job/**. **Project name**은 **unity-build**를 입력합니다.
{{% notice note %}}
Provider name은 여러분이 생성하신 Jenkins Job의 AWS Codepipeline step에서 입력하신 Provider 이름입니다.
그리고 Project name은 Jenkins Job name입니다.
{{% /notice %}}
(이미지)

5. **Add deploy stage**에서는 **Deploy provider**에서 **Amazon S3**를 선택합니다 **Region**은 여러분의 Region을 선택하시면 됩니다. Bucket을 선택합니다. 만약 Bucket이 없다면 S3 Console에서 생성하시면 됩니다. **Deployment path**에서는 unitybuild를 입력합니다. 그리고 **Extract file before deploy**를 체크한후 **NEXT**를 클릭합니다. 

6. 제대로 생성이 되었는지 리뷰하고, 이상이 없다면 **Create Pipeline**을 클릭하여 Pipeline을 생성합니다.
---
<p align="center">
© 2020 Amazon Web Services, Inc. 또는 자회사, All rights reserved.
</p>
