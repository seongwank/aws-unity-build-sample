---
title: AWS CodePipline 만들기 
weight: 40
pre: "<b>3. </b>"
---

{{% notice note %}}
본 Step에서는 AWS Codepipline을 만들고 Jenkins와 연동하는 작업이 진행됩니다. 모든 작업은 AWS console에서 진행됩니다.
{{% /notice %}}

## GitHub Repository fork 하기
먼저 AWS CodePipeline을 시작하기에 앞서, GitHub에 이 실습에서 사용할 Repository를 생성해야 합니다. 이미 이 실습을 진행하기 위한 Empty unity project가 준비되어 있습니다. [여기](https://github.com/seongwank/empty_unity_sample)를 클릭하여 Github repository 브라우저에 엽니다. 그리고 이 Repository를 여러분의 Account에 Fork하도록 합니다. 아래의 사진과 같이 Github page에서 **Fork** 버튼을 클릭하면 간단하게 여러분의 Git Account를 사용하여 AWS CodePipeline에 연결할 수 있습니다.
![Github]("/images/codepipeline/githubfork.png")

## AWS CodePipeline 생성하기

1. **AWS CodePipeline Console**의 **Create new pipeline**버튼을 클릭합니다.
![CodePipeline Console]("/images/codepipeline/pipelineconsole.png")

2. **Choose pipeline settings** 항목의 **pipeline name**에 `unity-build-pipeline`을 입력합니다. **Service role**은 **New Service role**을 선택하고 나머지 설정은 그대로 둡니다.
![CodePipeline Console]("/images/codepipeline/codepipelinesetting.png")

3. **Add source stage**의 **Source provider**에서는 **GitHub (Version 2)**을 선택합니다. Connection에서 **Connect to GitHub**을 클릭합니다. 
![CodePipeline Console]("/images/codepipeline/githubconnect.png")

4. **Create GitHub App connection** 의 Conenction name에서는 자유롭게 name을 작성하실 수 있습니다. 여기서는 간단하게 `my GitHub`이라고 작성하겠습니다. 작성 후 **Connect to GitHub**을 클릭합니다. 클릭 후 새로 나오는 창에서 **Authorize AWS Connector for GitHub**을 클릭합니다.
![CodePipeline Console]("/images/codepipeline/mygithub.png")

5. 아래의 그림과 같은 창이 뜨면 **Install a new app**을 클릭합니다.
![CodePipeline Console]("/images/codepipeline/githubinstallnew.png")

6. 아래와 같은 창이 뜨면, **All repositories**를 선택해도 되나 연결하고자하는 특정 Repository만 선택할 수 있습니다. 특정 Repository만 연결하고자 한다면 **Only select repositories**를 선택하고, [윗 단계]()에서 Fork한 **empty_unity_sample**을 선택합니다.
![CodePipeline Console]("/images/codepipeline/selectrepo.png")

7. **Repository name**에서는 이전 step에서 Fork한 Github Repository를 선택합니다.(**"your github account"/empty_unity_sample**) **Branch name**은 **main**를 선택합니다. **Change detection options**은 **Start the pipeline on source code change**를 **해제**합니다. **Output arthifact format에서는** **CodePipeline default**를 선택한 후 **Next**를 누릅니다.
![CodePipeline Console]("/images/codepipeline/setrepo.png")

4. **Build provider**에서 **Add Jenkins**를 선택합니다. **Provider name**은 `JenkinsProvider`을 입력합니다. **Server URL**에는 Step 2.3에서 테스트해본 Windows EC2 public DNS의 주소를 활용하여 입력합니다. **http://your-ec2-public-dns:8080/job/**. **Project name**은 `unity-android-build`를 입력합니다. 그리고 **Next**를 클릭합니다.
![CodePipeline Console]("/images/codepipeline/buildstage.png")
{{% notice info %}}
Provider name은 여러분이 생성하신 Jenkins Job의 AWS Codepipeline step에서 입력하신 Provider 이름입니다.
그리고 Project name은 Jenkins Job name입니다.
{{% /notice %}}

5. **Add deploy stage**에서는 **Deploy provider**에서 **Amazon S3**를 선택합니다 **Region**은 여러분의 Region을 선택하시면 됩니다(이 실습에서는 **ap-northeast-2**를 기준으로 진행합니다). 그리고 output artifacts를 저장할 Bucket을 선택합니다. 만약 Bucket이 없다면 아래의 그림과 같이 S3 Console에서 간단하게 생성하실 수 있습니다.
![CodePipeline Console]("/images/codepipeline/createbucket.png")

6. **Deployment path**에서는 `android-output`를 입력합니다. 그리고 **Extract file before deploy**를 체크한후 **NEXT**를 클릭합니다. 
![CodePipeline Console]("/images/codepipeline/deploystage.png")

7. 제대로 생성이 되었는지 리뷰하고, 이상이 없다면 **Create Pipeline**을 클릭하여 Pipeline을 생성합니다.
---
<p align="center">
© 2020 Amazon Web Services, Inc. 또는 자회사, All rights reserved.
</p>
