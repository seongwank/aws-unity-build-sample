---
title: 실습 2-3. Unity 설치하기
weight: 20
pre: "<b>3. </b>"
---

## Unity 설치
1. 원격으로 Windows EC2 instance를 접속하여 인터넷 브라우저에서 Unity Download 링크에 접속하여 **Unity Hub**를 다운로드 받습니다.[순서를 가이드합니다.](https://unity3d.com/get-unity/download)

2. Unity를 설치하는데는 특별한 설정이 필요없습니다. 기본 설정 그대로 설치를 완료합니다.

3. 설치가 완료되면 Unity Hub를 실행하여 **오른쪽 상단의 톱니바퀴(Preferences)**를 클릭합니다. 그리고 **License Management**의 **ACTIVATE NEW LICENSE**를 클릭합니다. 
   
4. **License Agreement**의 **Unity Personal**을 클릭합니다. 그리고 **I don't use Unity in a professional capacity**를 선택한 후 **DONE**을 클릭합니다.
{{% notice note %}}
만약 이미 License를 가지고 있다면, 새로운 Personal License대신 갖고 계신 License를 사용하셔도 괜찮습니다.
{{% /notice %}}

5. License가 활성화 되면, 왼쪽 상단의 **<- Preferences**를 클릭하고 **Installs**를 클릭합니다.

6. **ADD** 버튼을 클릭하여 **Recommended Release**에 있는 버전을 선택하고 **NEXT**를 클릭합니다.

7. **Add modules to your install** Step에서는 **Android Build Support**를 선택하고 **NEXT**를 클릭합니다.

8. 설치가 모두 완료되면 Jenkins Job을 생성할 준비가 되었습니다.


---
<p align="center">
© 2020 Amazon Web Services, Inc. 또는 자회사, All rights reserved.
</p>
