---
title: 실습 소개
weight: 10
pre: "<b>1. </b>"
---

이 실습은 AWS CodePipeline을 사용하여 여러분들의 Android Unity project를 빌드할 수 있는 Pipeline을 구성해보는 것입니다.
좀 더 구체적으로 Windows EC2에서 Unity project를 빌드할 수 있는 Jenkins 서버를 구축하고 AWS CodePipeline과 연동하여 S3에 APK파일을 생성하게 됩니다.
이 실습을 응용하면 Android뿐만 아니라 다른 빌드버전을 생성하여 Artifacts를 S3에 생성하실 수 있습니다!


이 워크샵은 크게 3가지 스텝으로 이루어져 있습니다.
1. EC2 instance를 사용하여 Windows 기반 Jenkins 서버를 구성합니다
2. Jenkins 서버와 여러분의 SourceCode를 AWS Codepipeline와 연동하여 Pipeline을 생성합니다
3. CodePipeline 생성을 마치고 실제로 어떻게 동작하는지 알아봅니다


---
<p align="center">
© 2021 Amazon Web Services, Inc. 또는 자회사, All rights reserved.
</p>
