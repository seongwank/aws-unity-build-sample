---
title: 2-2. Jenkins 설치하기
weight: 20
---

{{% notice note %}}
이 과정에서는 원격으로 Windows EC2에 접속을 한 후 진행하는 실습입니다.
{{% /notice %}}

## IE download 권한 허용
초기 Windows EC2 instance는 IE Enhanced Security Configuration이 활성화 되어있어서 File을 다운로드할 수 없습니다.
따라서 [다운도르 문제 해결 문서](https://aws.amazon.com/ko/premiumsupport/knowledge-center/ec2-windows-file-download-ie/?nc1=h_ls)의 **해결 방법**을 따라하여 다운로드가 가능하도록 IE 설정을 변경합니다.
![IE allow download](/images/ec2/allowdownload.png)



## Java 설치
1. 다운로드 권한을 활성화 시켰다면 Jenkins를 설치하기 위해 먼저 Java JDK를 설치해야 합니다. Windows x64 product의 JDK 8을[다운로드](https://www.oracle.com/kr/java/technologies/javase/javase-jdk8-downloads.html)받습니다.
![JDK8 Download](/images/ec2/jdk8download.png)
{{% notice info %}}
본 실습에서는 JDK 8 버전을 사용합니다.
또한 Java를 다운로드 받기 위해서는 Oracle 계정이 필요합니다. 계정을 생성하고 로그인하면 다운로드가 가능합니다.
{{% /notice %}}

3. File explorer에서 Download 폴더의 jdk-8uxxx-windows-x64를 더블클릭하여 설치를 진행 합니다.

3. 설치가 완료되면 환경 변수를 설정합니다. 
   + 먼저 Windows창 왼쪽 하단의 검색 버튼을 클릭합니다. 그리고 **edit the system environment variables**를 타이핑 합니다. 
   + 검색해서 나온 Control panel을 클릭합니다. 
   + **System properies** 창이 실행되면 **Advanced -> Environment Variables**를 클릭합니다. 
   + 그리고 **System variables**의 항목에서 **path**를 더블 클릭합니다. 
   + **Edit environment variable**창이 실행되면 오른쪽 버튼들 중 **new**를 클릭하여 JDK가 설치된 folder를 입력합니다. 여러분이 과정을 그대로 따라하였다면 JDK의 위치는 다음과 같습니다. `c:\Program Files\Java\jdk1.8.0_xxx\bin` 
   + **OK**를 눌러 설정을 마칩니다.
![JDK 환경 변수 설정](/images/ec2/jdkpath.png)



## Jenkins 설치
1. JDK가 설치가 완료되면 Jenkins를 설치하실 수 있습니다. 먼저 Jenkins의 **Windows** 버전을 [다운로드](https://www.jenkins.io/download/)받습니다.
![Jenkins Download](/images/ec2/jenkinsdownload.png)
{{% notice info %}}
본 실습에서는 2.263.3 LTS 버전을 사용하였습니다. 이 버전이 실습을 수행하기 위한 필수 버전은 아닙니다. 다른 2.xxx.x 버전을 다운로드 받으셔도 실습을 수행하실 수 있습니다.
{{% /notice %}}

2. Jenkins를 다운로드 받은 후 File explorer에서 Download 폴더의 **jenkins**를 실행하여 설치를 합니다.
{{% notice info %}}
설치 중 **Service Logon Credentials** Step에서는 **Run service as local or domain user:**를 선택합니다. 그리고 Account는 `Administrator`이고 Password는 **EC2 Console에서 RDP client로 접근하기 위해 열람한 Password**입니다.
{{% /notice %}}
![Jenkins 설치 실패 화면](/images/ec2/jenkinsprivilege.png)
   #### 만약 위 그림과 같이 설치가 실패한다면 아래의 과정을 거쳐 문제를 해결하실 수 있습니다.
   + Windows 왼쪽 하단의 Search(돋보기 모양)을 클릭하고 **Administrative Tools**를 검색하고 **Local Security Policy**를 실행합니다.
   + **Local Policies**를 클릭하고, **User Rights Assignment**를 클릭합니다.
   + 오른쪽 panel에서 **Log on as a service** 항목을 오른쪽 클릭을하여 **properties**를 선택합니다.
   + **Add User or Group**을 클릭하고 Enter **the object names to select**에서 **administrator**를 입력하고 **Check Names**를 클릭한 후 **OK**를 클릭합니다.
   ![Allow port](/images/ec2/allowprivilege.png)

3. Jenkins 설치가 완료되면 완료 창에서 시작 버튼을 눌러 Jenkins를 실행합니다.

4. 원격으로 접근한 Windows EC2 instance에서 인터넷 브라우저를 열어 **localhist:8080**에 접근합니다. **Unlock Jenkins** 에서능 **initialAdminPassword** file을 Notepad에서 열어 Administrator password를 얻어 입력합니다. **Customize Jenkins**에서는 **Install suggested plugins**를 선택합니다. 모든 설정을 완료하고 **Save and Finish**를 눌러 설치를 마칩니다.
![Jenkins admin](/images/ec2/jenkinsadmin.png)

5. 4번까지 진행하면, Jenkins 설치가 모두 완료가 되었습니다. 하지만 Local PC와 Codepipeline이 접근하기 위해서는 Windows의 port를 열어 접근할 수 있도록 조치를 취해야 합니다. 
   - Windows 왼쪽 하단의 Search(돋보기 모양)를 클릭합니다. 
   - **Windows Defender Firewall**을 타이핑하고 **Windows Firewall control panel**를 클릭합니다.
   - 왼쪽 프레임의 **Advanced settings**를 선택합니다.
   - 왼쪽 프레임의 **Inbound Rules**를 클릭합니다. 그리고 오른쪽 프레임의 **New Rule...**을 클릭합니다.
   - **Port**를 선택하고 **Next**를 클릭합니다.
   - **TCP**를 선택하고 **Specific local ports**를 클릭하고 `8080`을 입력한 후 **Next**를 클릭합니다.
   - **Allow the connection**을 선택하고 **Next**를 클릭합니다.
   - **Public**을 선택하고 **Next**를 클릭합니다.
   - **Name**에 `Jenkins port`를 입력하고 **Finish**를 클릭합니다.
![Allow port](/images/ec2/allowport.png)

6. Port가 제대로 연결되었는지 확인하기 위하여 Windows EC2 instance의 Public DNS를 이용하여 테스트해봅니다.
Public DNS는 AWS console의 **EC2 dashboard -> Running Instances -> Windows EC2 선택 -> Description의 Public DNS(IPv4)** 에서 확인하실 수 있습니다.
![Public DNS](/images/ec2/publicdns.png)

{{% notice warning %}}
혹시 public DNS로 jenkins에 접근이 가능하지 않다면, Local PC에서 실행중인 VPN등의 시스템이 8080 port를 차단하고 있는지 확인이 필요합니다.
{{% /notice %}}




---
<p align="center">
© 2020 Amazon Web Services, Inc. 또는 자회사, All rights reserved.
</p>