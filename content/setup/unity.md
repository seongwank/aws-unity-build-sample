---
title: 2-3. Unity 설치하기
weight: 20
---

## Unity 설치
1. 원격으로 Windows EC2 instance를 접속하여 인터넷 브라우저에서 Unity Download 링크에 접속하여 **Unity Hub**를 [다운로드](https://unity3d.com/get-unity/download) 받습니다.
![Unity Download](/images/ec2/unitydownload.png)

2. Unity를 설치하는데는 특별한 설정이 필요없습니다. 기본 설정 그대로 설치를 완료합니다.

3. 설치가 완료되면 Unity Hub를 실행하여 **오른쪽 상단의 톱니바퀴-Preferences**를 클릭합니다. 그리고 **License Management**를 클릭하고 하단의 **Manage License**를 클릭 그리고 연속하여 **Login**을 클릭하여 Log-in을 진행합니다. **ACTIVATE NEW LICENSE**를 클릭합니다. 
{{% notice info %}}
Unity License를 얻기 위해서는 Unity 계정이 필요합니다. 계정이 없다면 이 과정을 통하여 새로운 계정을 생성하실 수 있습니다.
{{% /notice %}}

4. **License Agreement**의 **Unity Personal**을 클릭합니다. 그리고 **I don't use Unity in a professional capacity**를 선택한 후 **DONE**을 클릭합니다.
![Unity License](/images/ec2/unitygetlicense.png)
![Unity License](/images/ec2/unitylicense.png)
---
{{% notice info %}}
만약 이미 License를 가지고 있다면, 새로운 Personal License대신 갖고 계신 License를 사용하셔도 괜찮습니다.
{{% /notice %}}

5. License가 활성화 되면, 왼쪽 상단의 **<- Preferences**를 클릭하고 **Installs**를 클릭합니다.

6. **ADD** 버튼을 클릭하여 **Recommended Release**에 있는 버전을 선택하고 **NEXT**를 클릭합니다.
![Add Unity Version](/images/ec2/unityversion.png)

7. **Add modules to your install** Step에서는 **Android Build Support**를 선택하고 **NEXT**를 클릭합니다.
![Add Unity Version](/images/ec2/unityinstall.png)
![Install Unity](/images/ec2/unityinstall2.png)
---

{{% notice warning %}}
만약 용량이 부족하여 설치가 되지 않는다면 [여기](https://aws.amazon.com/ko/premiumsupport/knowledge-center/expand-ebs-root-volume-windows/)를 참고하여 EBS volume을 확장할 수 있습니다.
{{% /notice %}}

8. 설치가 모두 완료되면 Jenkins Job을 생성할 준비가 되었습니다.





---
<p align="center">
© 2020 Amazon Web Services, Inc. 또는 자회사, All rights reserved.
</p>