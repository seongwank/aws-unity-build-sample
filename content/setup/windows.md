---
title: EC2 Windows & RDP client 설치하기
weight: 21
pre: "<b>2-1. </b>"
---

## EC2에 적용할 IAM role 생성
{{% notice note %}}
EC2 Windows를 생성하는 이유는 CodePipeline과 연동할 수 있는 Jenkins 서버를 구성하는 목적입니다. 따라서 EC2 instance가 CodePipeline과 연동하기 위한 권한을 먼저 생성하고, EC2 instance에 적용할 수 있도록 합니다.
{{% /notice %}} 
1. [IAM role console](https://console.aws.amazon.com/iam/home)에 접근합니다. 그리고 왼쪽 패널의 **Roles**를 클릭한 후, **Create Role**을 클릭합니다.
![IAM Role](/images/ec2/createrole.png)

2. 그리고 **Select type of trusted entity**항목에서 **AWS service**를 클릭하고, **Choose a use case**에서 **EC2**를 클릭한 후 **Next: Permissons**버튼을 눌러 다음으로 넘어갑니다.
![IAM Role](/images/ec2/createec2role.png)

3. 다음으로 검색창에서 `AWSCodePipelineCustomActionAccess`를 검색하여 선택한 후 **Next: Tags**버튼을 눌러 다음으로 넘어갑니다.
![IAM Role](/images/ec2/selectpipelinerole.png)

4. **Add tags**부분에서는 이 실습에서는 아무것도 입력하실 필요가 없습니다. **Next: Review**버튼을 클릭하여 다음으로 넘어갑니다.
![IAM Role](/images/ec2/selectpipelinerole.png)

5. 마지막으로 **Review**에서는 **Role name**에 `ec2-windows-jenkins-role`을 입력한 후 **Create role**버튼을 클릭하여 IAM role 생성을 마칩니다.




## EC2 Windows Server Launch 
{{% notice note %}}
이 과정은 EC2 Instance를 생성하기 위한 것입니다. 꼭 이 과정을 따라서 생성하실 필요는 없습니다. 다만 Unity Build를 위한 Jenkins 서버를 구성하기 위한 과정입니다. 따라서 Unity Build를 위한 충분한 Instance type, storage를 고려하셔서 생성하시는 걸 추천드립니다. 
{{% /notice %}} 

1. EC2 Dashboard 에서 **Launch instance** 버튼을 클릭합니다.
![EC2 dashboard](/images/ec2/ec2dashboard.png)

2. EC2 생성 페이지의 **Step 1: Choose an Amazon Machine Image - AMI**에서 Windows AMI를 선택합니다. 이 실습에서는 **Microsoft Windows Server 2019 Base - ami-0ff0049cd3c9a5fcb** 를 선택하겠습니다.
{{% notice info %}}
물론 꼭 이 버전의 Windows Server AMI를 선택해야 하는 것은 아닙니다. Jenkins, Unity가 설치 가능한 다른 Windows 버전 AMI를 선택 하실 수 있습니다.
{{% /notice %}} 

3. Instance Type을 선택합니다. 여기서는 **c5large**를 선택하였습니다.
{{% notice info %}}
이 역시 다른 type의 Instance를 선택하셔도 괜찮습니다. 다만 Unity Build를 위한 Jenkins 서버를 구축하는 목적임을 고려하여 적당한 타입의 Instance를 선택하는 것이 좋습니다. 이 실습을 위한 EC2 Instance라면, 실행하는 Build는 Empty Project이니 크게 무거운 작업이 아니기 때문에 너무 높은 Instance Type을 선택하실 필요는 없습니다.
{{% /notice %}} 

4. 다음으로 **Configure Instance Details** 입니다. 여기서 설정하셔야 하는 부분은 **Network**, **Subnet**입니다. 
   + **Network**는 VPC를 선택하는 곳입니다. 여러분의 Console에서 생성된 VPC중 적절한 VPC를 골라 설정합니다, 그렇지 않다면 AWS 계정을 생성했을 때 기본으로 생성된 **default VPC**를 선택합니다. 
   + **Subnet**도 마찬가지로 여러분이 이미 생성한 Subnet중에서 선택할 수 있습니다. 만약 생성한 Subnet이 없다면 **Create new subnet** 을 선택하여 새로운 Subnet을 생성합니다. Subnet을 생성할때 **AZ - Availability Zone** 은 Region내에 존재하는 AZ 중 아무거나 선택하셔도 괜찮습니다. 
   + **IAM role**항목에서는 여러분이 윗 단계에서 생성하신 `ec2-windows-jenkins-role`를 찾아 선택합니다.

5. 나머지 설정은 이 실습을 진행하는데 큰 의미가 없습니다. 따라서 그대로 놔두고 **Next:Add Storage**를 클릭합니다.

6. **Step. 4 Storage**는 Unity3d 설치를 위해 **Root Volume type**의 **Size**를 **최소 30gb 이상**으로 설정하는 것이 좋습니다. 그리고 **Next:Add Tag**를 클릭합니다.

7. **Next:Add Tag**에서는 아무것도 입력하지 않고, **Next:Configure Security Group**를 클릭합니다.

8. **Step 6: Configure Security Group**은 총 2개의 Inbound Rule을 추가합니다.
   + Type: RDP, Protocol: TCP, Port Range:3389, Source: Custom 0.0.0.0/0
   + Type: Custom TCP Rule, Potocol: TCP, Port Range:8080, Source: Custom 0.0.0.0/0
![Inbound Rules](/images/ec2/ec2inbound.png)

9. 입력을 마치면 **Review and Launch** 를 클릭 후, 제대로 입력이 되었는지 리뷰 후 **Launch**를 누릅니다.

10. 마지막으로 EC2 instance에 접근할 수 있는 key pair를 선택하는 Step입니다. 만약 이미 사용하고 있는 key pair가 있다면 **Choose an existing key pair**를 선택하여 이미 갖고있는 key pair를 선택하면 됩니다. 만약 새로운 key pair가 필요하다면 **Create a new key pair**를 선택하여 key pair name을 입력 후 **Download Key Pair**를 클릭하여 file을 Local PC에 다운로드 합니다.
{{% notice warning %}}
Download된 pem file은 본 실습에서 원격으로 Windows에 접속할때 꼭 필요합니다.
{{% /notice %}}

11. EC2 instance의 생성이 완료되었습니다!


## RDP Client 설치 및 연결
{{% notice note %}}
이 과정은 RDP client를 Local PC에 설치하기 위한 과정입니다. 2-2 Jenkins 설치, 2-3 Unity 설치는 RDP client로 EC2 instance GUI환경에 접근한 후 진행됩니다.
{{% /notice %}} 

1. 먼저 RDP로 접근할 수 있는 Password를 확인해야 합니다. **EC2 Dashboard -> INSTANCES -> Instances** 항목에서 생성한 Windows EC2 instance를 선택하고 **Connect** 버튼을 클릭합니다. 
![Connect](/images/ec2/ec2connect.png)

2. 먼저 **Connect to your instance** 창에서 **Download Remote Desktop File**을 클릭하여 EC2 instance에 접근할 수 있는 rdp file을 획득합니다.

3. 그리고 **Get Password**를 클릭합니다. 클릭하고 EC2 인스턴스를 생성하면서 선택한 **pem file**을 업로드합니다. 업로드를 하고 **Decrypt Password**를 클릭하면 password를 획득할 수 있습니다. 이 password를 저장해 둡니다. 

4. [RDP Client](https://docs.microsoft.com/ko-kr/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients)를 Local PC에 설치합니다. 

5. **Microsoft Remote Desktop**을 제대로 설치하였다면 2. 에서 다운로드 받았던 rdp file을 실행합니다.
![RDP](/images/ec2/rdp.png)

6. 3. 에서 저장한 Password를 입력하면 EC2 Windows instance의 GUI 환경으로 접속하실 수 있습니다.

7. 접속 후 **Network** 허용 창이 뜨면 **Yes**를 누릅니다.






---
<p align="center">
© 2021 Amazon Web Services, Inc. 또는 자회사, All rights reserved.
</p>
