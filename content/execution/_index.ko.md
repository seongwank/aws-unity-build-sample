---
title: AWS CodePipeline 실행하기
weight: 40
pre: "<b>4. </b>"
---

{{% notice note %}}
이 단계에서는 위에서 완료한 CodePipeline의 생성을 완료하고, 실행 과정을 살펴보는 실습입니다. 
{{% /notice %}}

## AWS CodePipeline 실행하기

1. CodePipeline 생성을 마치면 자동으로 pipeline이 실행이 되어 Source 단계가 In progress라고 변경되는 것을 확인하실 수 있습니다. 
![codepipeline](/images/execution/initialexecution.png)
{{% notice info %}}
여러분이 직접 pipeline을 실행해보시려면 **Release change**를 누르시면 pipeline이 실행됩니다. 또한 이 실습에서는 다루지 않았지만 CodePipeline을 자동으로 실행하고자 한다면 [이 문서](https://docs.aws.amazon.com/codepipeline/latest/userguide/pipelines-about-starting.html#change-detection-methods)나 [CodePipeline의 notification rule](https://docs.aws.amazon.com/dtconsole/latest/userguide/getting-started-pipeline.html)에서 설정하실 수 있습니다.
{{% /notice %}}

2. Source 단계가 성공적으로 완료되면 Build 단계가 In progress상태로 변하여 진행 중 인것을 알 수 있습니다. 여기서 Jenkins의 동작 상태를 확인해보시려면 **Custom android-build-provider**를 클릭하면 Jenkins Job 페이지로 전환됩니다.
![codepipeline](/images/execution/jenkins.png)

3. Build 단계가 끝나고 Deploy 단계까지 끝나면 아래 그림과 같이 모든 단계가 **Succeeded**라고 표시됩니다.
![codepipeline](/images/execution/pipeline.png)

4. S3에 빌드가 완료된 artifacts를 확인해보시려면 Deploy 단계의 **Amazon S3**를 클릭하면 S3 bucket으로 접속해서 artifacts를 확인할 수 있습니다.
![codepipeline](/images/execution/s3.png)

<!--앞으로 해야할일
AMI로 설치과정을 간단하게 만들기,
Mac instance가 나오면 ios빌드까지 추가하기
test 환경으로 자동으로 artifacts가 입력되고 알림보내기(aws device farm)
-->
<p align="center">
© 2021 Amazon Web Services, Inc. 또는 자회사, All rights reserved.
</p>


