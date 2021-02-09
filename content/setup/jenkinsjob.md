---
title: 2-4. Unity Build Job 생성하기
weight: 20
---
{{% notice note %}}
한국어로 설정된 Local PC에서 public DNS로 젠킨스에 접속하시면 한글로 번역된 Jenkins 화면을 보실 수 있습니다.
하지만 이 실습에서 설정한 EC2 instance에서 localhost로 접근하셨을때는 영문으로 된 Jenkins 화면이 보입니다.
각 항목들이 헷갈리시지 않도록 한글-영문으로 구분되어 보이는 항목들은 한글-영문을 모두 병기하였으니 참고하셔서 실습하시면 됩니다. 
{{% /notice %}}

## Jenkins Install plug-ins & Configuration

1. 이제 Jenkins를 열어 플러그인과 설정을 합니다. 
{{% notice info %}}
원격으로 접속해서 설정할때는 **localhost:8080**으로 접근하고, Local PC에서 Jenkins를 설정하시려면 **Your EC2 public DNS adderess:8080**으로 접근하시면 됩니다.
{{% /notice %}}
2. Jenkins에 접속하셨으면 **Jenkins 관리-Manage Jenkins**를 클릭한 다음, **플러그인 관리-Manage Plugins**를 클릭하고 **설치가능-Available** 탭을 클릭합니다. 
![Install CodePipeline](/images/ec2/awspipeline.png)

3. **AWS CodePipeline**를 검색하고 **왼쪽 체크 박스**를 클릭합니다. 그리고 **Unity3d plugin**를 검색하고 **왼쪽 체크 박스**를 클릭합니다. 그리고 맨 하단의 **재시작 없이 설치하기-Install without restart**를 클릭하여 설치를 완료합니다.
![Install CodePipeline](/images/ec2/unityplugin.png)

1. 설치가 완료되면 다시 첫 화면에서 **Jenkins 관리**를 클릭하고 **Global Tool Configuration**를 클릭합니다.

2. **Unity3d** 항목의 **Unity3d installations**를 클릭합니다. **Add Unity3d**를 클릭하고 **Name**에 `Unity 2019.xx.xxf(your version)`를 입력합니다. 그리고 **Installation directory**에 설치된 Unity의 Path를 입력합니다.

{{% notice info %}}
이 과정까지 실습과 동일하게 따라오셨다면 Unity Directory Path는 `C:\Program Files\Unity\Hub\Editor\20xx.x.xxfx`입니다. 그렇지 않다면 여러분이 Unity를 설치한 Drectory Path를 입력합니다.
{{% /notice %}}




## Jenkins Unity Build Job 생성

1. Jenkins의 첫화면에서 왼쪽 frame에 있는 **새로운 Item-New item**을 클릭합니다. 

2. **Enter an item name** field에 `unity-android-build`라고 입력한 후, 하단의 **Freestyle proeject**를 선택하고 **OK**를 누릅니다. 

3. Job 생성화면에서 **소스 코드 관리-Source Code Management** 탭에서 **AWS CodePipeline**를 선택합니다.

4. **AWS Region**에서 여러분의 Region을 선택합니다. 이번 실습에서는 **Asia Pacific(Seoul) ap-northeast-2**를 선택하였습니다. 그리고 **Category**에서는 `Build`를 선택합니다. 마지막으로 **Provider**는 `android-build-provider`를 입력합니다. 그외에는 아무것도 입력하지 않고 그대로 냅두셔도 괜찮습니다.
![CodePipeline setting](/images/ec2/awscodepipeline.png)
{{% notice info %}}
**Provider**는 CodePipeline의 Build 설정에 꼭 필요한 변수입니다. 
{{% /notice %}}

5. **빌드 유발-Build Triggers**에서 **Poll SCM**을 선택하고 `* * * * *`를 입력합니다.
![Build Triggers](/images/ec2/pollscm.png)

6. **Build**에서 **Add build step**을 선택한 다음, **Invoke Unity3d Editor**를 클릭합니다. 

7. **Unity3d installation name**에서 여러분이 **Global Configuration**에서 입력한 **Unity3d Editor**를 선택합니다.

8. **Editor command line arguments**에 `-quit -batchmode -executeMethod Builder.PerformAndroidBuild -logFile "C:\Users\Administrator\Documents\android_build.log"`를 입력합니다.

9.  다시 한번 **Add build step**을 선택하고, **Execute Windows batch command**를 클릭합니다.

10. **Command** field의 첫번째 라인에 `mkdir apk`, 두번째 라인에 `move android_build_lab.apk apk/android_build_lab.apk`를 입력합니다.
![Jenkins Job Build Step](/images/ec2/jenkinsjobbuildstep.png)

11. 마지막으로 **빌드 후 조치-Post-build Actions**항목에서 **빌드 후 조치 추가-Add post-build action**을 클릭한 후 **AWS CodePipeline Publisher**를 클릭합니다. 그리고 **Location** field에 `/apk/`를 입력합니다. **Artifact Name** field에는 `BuildArtifact`를 입력합니다.
![Jenkins Post Build Step](/images/ec2/jenkinspostbuild.png)
{{% notice note %}}
**Artifact Name**는 CodePipeline의 Build 설정에 꼭 필요한 변수입니다. 
{{% /notice %}}

12.  가장 하단의 **저장(Save)** 버튼을 클릭하여 Jenkins Job 생성을 완료합니다.




---
<p align="center">
© 2020 Amazon Web Services, Inc. 또는 자회사, All rights reserved.
</p>
