---
title: 사전 준비
weight: 11
pre: "<b>1-1. </b>"
---

1. 이 실습은 AWS console에서 진행이 됩니다. 따라서 이미 사용하고 계신 AWS 계정이나 [새로운 AWS 계정](https://aws.amazon.com/ko/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc)을 생성하셔야 합니다. 

2. Unity Build를 해보기 위해서는 먼저 SourceCode가 필요합니다. 이 실습에서는 쉽게 따라하실 수 있도록 빈 Unity 프로젝트를 GitHub에 생성해 놓았습니다. GitHub 계정이 있어야 GitHub 프로젝트를 사용하여 AWS CodePipeline과 연동하실 수 있습니다. 계정이 없으시다면 [여기](https://github.com/join?ref_cta=Sign+up&ref_loc=header+logged+out&ref_page=%2F&source=header-home)에서 간단하게 생성하실 수 있습니다.

3. Build 서버는 Windows EC2 instance로 구성합니다. 따라서 Windows에 원격으로 접속하기 위한 [Microsoft Remote Desktop](https://docs.microsoft.com/ko-kr/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients)을 설치하셔야 원활한 실습 진행이 가능합니다. 여러분의 Local PC가 [Microsoft Remote Desktop](https://docs.microsoft.com/ko-kr/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients)을 설치할 수 있는 환경인지 확인해보세요.

4. 마지막으로 [AWS CodePipeline](https://aws.amazon.com/ko/codepipeline/), [Unity](https://unity.com/kr), [Jenkins](https://www.jenkins.io/)에 관한 간단한 지식입니다. 물론 이 실습은 해당 지식이 없어도 진행이 가능합니다. 하지만 실습에 사용되는 서비스와 어플리케이션이 어떤 역할을 하는지 미리 알고 진행하신다면 더욱 쉽게 실습을 진행하실 수 있습니다.


---
<p align="center">
© 2021 Amazon Web Services, Inc. 또는 자회사, All rights reserved.
</p>
