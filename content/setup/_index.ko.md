---
title: Jenkins Build Server 구성
weight: 30
pre: "<b>2. </b>"
---
**본 실습은 Window OS에서 Jenkins를 활용하여 Unity Build Server를 구축하기 위한 과정입니다. 아래와 같이 4개의 주제로 이루어져 있습니다. 4가지 주제 모두 따라하셔야 workshop을 정상적으로 진행하실 수 있습니다.** <br/><br/>

{{% notice warning %}}
이 부분이 가장 할일이 많습니다. 하지만 Code pipeline 설정과 테스트는 그렇지 않으니 너무 걱정하지 마세요
{{% /notice %}}

### 목차 
1. EC2 Windows & RDP client 설치하기
2. Jenkins 설치하기
3. Unity 설치하기
4. Jenkins Unity Build Job 생성하기

{{% notice warning %}}
프리 티어 유지를 위해서 인스턴스 타입을 ***t2.micro*** 에서 변경하지 않습니다.
{{% /notice %}}

{{% notice info %}}
키 쌍(Key Pairs)는 각 리전(Region)별로 독립적으로 관리됩니다.
{{% /notice %}}

---
<p align="center">
© 2020 Amazon Web Services, Inc. 또는 자회사, All rights reserved.
</p>
