---
title: 실습 2-2. Jenkins 설치하기
weight: 20
pre: "<b>2. </b>"
---

{{% notice note %}}
이 과정에서는 원격으로 Windows EC2에 접속을 한 후, Windows EC2에서 진행하는 실습입니다. download가 필요한 부분이 있어서 먼저 IE의 download 권한을 허용해야합니다.
{{% /notice %}}

## IE download 권한 허용
만약 Windows EC2 instance의 IE(Internet Explorer)의 다운로드 권한이 Disable되어있다면, Lab을 진행할 수 없습니다.
따라서 아래와 같은 절차로 다운로드 권환을 활성화 시킵니다.
**Internet Options -> Security Settings -> File download -> disable 에서 enable로 변경**  

## Java 설치
1. 다운로드 권한을 활성화 시켰다면 Jenkins를 설치하기 위해 먼저 Java JDK를 설치해야 합니다. Windows x64 product의 Download 링크를 클릭하여 다운로드합니다. [JDK 다운로드 링크](https://www.oracle.com/kr/java/technologies/javase/javase-jdk8-downloads.html)
{{% notice note %}}
본 Lab에서는 JDK 8 버전을 사용합니다.
또한 Java를 다운로드 받기 위해서는 Oracle 계정이 필요합니다. 계정을 생성하고 로그인하면 다운로드가 가능합니다.
{{% /notice %}}

1. File explorer에서 Download 폴더의 jdk-8uxxx-windows-x64를 실행하여 설치를 합니다.

2. 설치가 완료되면 환경 변수를 설정합니다. 먼저 Windows창 왼쪽 하단의 검색 버튼을 클릭합니다. 그리고 **edit the system environment variables**를 타이핑 합니다. 검색해서 나온 Control panel을 클릭합니다. **System properies** 창이 실행되면 **Advanced -> Environment Variables**를 클릭합니다. 그리고 **System variables**의 항목에서 **path**를 더블 클릭합니다.
**Edit environment variable**창이 실행되면 오른쪽 버튼들 중 **new**를 클릭하여 JDK가 설치된 folder를 입력합니다.
{{% notice note %}}
Environment variable path 예) c:\Program Files\Java\jdk1.8.0_xxx\bin
{{% /notice %}}
![JDK 환경 변수 설정](/images/ec2/jdkpath.png)


## Jenkins 설치
1. JDK가 설치가 완료되면 Jenkins를 설치하실 수 있습니다. 링크를 참조하여 Jenkins의 windows 버전을 다운로드 받으실 수 있습니다.[다운로드 링크](https://www.jenkins.io/download/)
{{% notice note %}}
본 Lab에서는 2.263.3 LTS 버전을 사용하였습니다. 꼭 이 버전이 아니더라도 2.xxx.x 버전을 다운로드 받으셔도 Lab을 수행하는데 어려움이 없습니다.
{{% /notice %}}

2. Jenkins를 다운로드 받은 후 File explorer에서 Download 폴더의 **jenkins**를 실행하여 설치를 합니다.
{{% notice warning %}}
권한이 없어서 설치가 불가능하다면 아래의 과정을 거쳐 문제를 해결하실 수 있습니다.
- Windows 왼쪽 하단의 검색창에서 **Administrative Tools**를 검색하고 **Local Security Policy**를 실행합니다.
- **Local Policies**를 클릭하고, **User Rights Assignment**를 클릭합니다.
- 오른쪽 panel에서 **Log on as a service** 항목을 오른쪽 클릭을하여 **properties**를 선택합니다.
- **Add User or Group**을 클릭하고 Enter **the object names to select**에서 **administrator**를 입력하고 **Check Names**를 클릭한 후 **OK**를 클릭합니다.
{{% /notice %}}

3. Jenkins 설치가 완료되면 완료 창에서 시작 버튼을 눌러 Jenkins를 실행합니다.

4. 원격으로 접근한 Windows EC2 instance에서 인터넷 브라우저를 열어 **localhist:8080**에 접근합니다. **Unlock Jenkins** 에서 **initialAdminPassword** file에서 Administrator password를 얻어 입력합니다. **Customize Jenkins**에서는 **Install suggested plugins**를 선택합니다. 모든 설정을 완료하고 **Save and Finish**를 눌러 설치를 마칩니다.

5. 4번까지 진행하면, Jenkins 설치가 모두 완료가 되었습니다. 하지만 Local PC와 Codepipeline이 접근하기 위해서는 Windows의 port를 열어 접근할 수 있도록 조치를 취해야 합니다. 
   - Windows 오른쪽 하단의 Search를 클릭합니다. 
   - **Windows Firewall**을 타이핑하고 **Windows Firewall control panel**를 클릭합니다.
   - **Advanced settings**를 선택합니다.
   - 왼쪽 프레임의 **Inbound Rules**를 클릭합니다. 그리고 오른쪽 프레임의 **New Rule...**을 클릭합니다.
   - **Port**를 선택하고 **Next**를 클릭합니다.
   - **TCP**를 선택하고 **Specific local ports**를 클릭하고 **8080**을 입력한 후 **Next**를 클릭합니다.
   - **Allow the connection**을 선택하고 **Next**를 클릭합니다.
   - **Public**을 선택하고 **Next**를 클릭합니다.
   - **Name**에 **Jenkins port**를 입력하고 **Finish**를 클릭합니다.

6. Port가 제대로 연결되었는지 확인하기 위하여 Windows EC2 instance의 Public DNS를 이용하여 테스트해봅니다.
{{% notice note %}}
Public DNS는 AWS console의 EC2 dashboard -> Running Instances -> Windows EC2 선택 -> Description의 Public DNS(IPv4) 에서 확인하실 수 있습니다.
ex) http://ec2-xx-xxx-xx-xx.ap-northeast-2.compute.amazonaws.com:8080/
{{% /notice %}}


---
<p align="center">
© 2020 Amazon Web Services, Inc. 또는 자회사, All rights reserved.
</p>
