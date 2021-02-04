---
title: 실습 2-1. EC2 Windows & RDP client 설치하기
weight: 20
pre: "<b>1. </b>"
---

## EC2 Windows Server Launch 

1. EC2 Dashboard 에서 **Launch instance** 버튼을 클릭합니다.

2. AMI를 선택합니다. 이 Lab에서는 **Microsoft Windows Server 2019 Base - ami-0ff0049cd3c9a5fcb** 를 선택하겠습니다.
{{% notice note %}}
물론 꼭 이 버전의 Windows Server AMI를 선택해야 하는 것은 아닙니다. Jenkins, Unity가 설치 가능한 다른 Windows 버전 AMI를 선택 하실 수 있습니다.
{{% /notice %}} 

3. Instance Type을 선택합니다. 여기서는 m5large를 선택하였습니다.

4. 다음으로 **Configure Instance Details** 입니다. VPC는 여러분의 VPC중 원하는 VPC를 골라 설정합니다, 아니라면 default VPC를 선택합니다. Subnet도 마찬가지로 여러분이 생성한 Subnet중에서 선택할 수 있습니다. 만약 Subnet이 없다면 **Create new subnet** 을 선택하여 새로운 Subnet을 생성합니다. (Availability Zone은 아무거나 선택해도 관계없습니다)

5. 나머지 설정은 이 Lab을 진행하는데 큰 의미가 없습니다. 따라서 그대로 놔두고, **Next:Add Storage**를 클릭합니다.

6. Storage는 Unity3d 설치를 위해 최소 30gb 이상으로 설정하는 것이 좋습니다.

7. **Next:Add Tag**는 Skip하고 **Next:Configure Security Group**를 클릭합니다.

8. Security Group은 총 2개의 Inbound Rule을 추가합니다.
   1. Type: RDP, Protocol: TCP, Port Range:3389, Source: Custom 0.0.0.0/0
   2. Type: Custom TCP Rule, Potocol: TCP, Port Range:8080, Source: Custom 0.0.0.0/0

9. **Review and Launch** 를 클릭 후, 리뷰 후 **Launch**를 누릅니다.

10. 만약 이미 사용하고 있는 key pair가 있다면 **Choose an existing key pair**를 선택하여 이미 갖고있는 key pair를 선택하면 됩니다. 만약 새로운 key pair가 필요하다면 **Create a new key pair**를 선택하여 key pair name을 입력 후 **Download Key Pair**를 클릭하여 file을 Local PC에 다운받습니다.
{{% notice warning %}}
Download된 pem file은 RDP로 접속할때 꼭 필요합니다.
{{% /notice %}}

11. EC2 instance의 생성이 완료되었습니다!

## RDP Client 설치 및 연결

1. 먼저 RDP로 접근할 수 있는 PW를 확인해야 합니다. **EC2 Dashboard -> INSTANCES -> Instances** 항목에서 생성한 Windows EC2 instance를 선택하고 **Connect** 버튼을 클릭합니다. 

![Connect](/images/ec2/ec2connect.png)

1. 그리고 Get Password를 클릭합니다. 클릭하고 EC2 인스턴스를 생성하면서 생성하였거나 사용했던 pem file을 업로드합니다. 업로드를 하고, Decrypt Password를 클릭하여 password를 획득합니다. 

2. RDP Client를 Local PC에 설치합니다. [다운로드 링크](https://www.microsoft.com/ko-kr/p/microsoft-remote-desktop/9wzdncrfj3ps)

3. **Microsoft Remote Desktop**을 제대로 설치하였다면 실행하여 Add PC를 클릭합니다.

4. PC name에는 여러분의 Windows EC2 instance의 **Public DNS**를 입력합니다. **Public DNS**는 EC2 Console에서 instance를 클릭한 후, Description에서 확인하실 수 있습니다. User account에서는 **Add User Account**를 클릭하고, Username에는 **Administrator**, Password에는 **step 2. 에서 획득한 password**를 입력한 후 Add 버튼을 클릭합니다.

5. 여러분의 Remote PC 설정이 끝났다면 더블클릭을 하여 EC2 instance GUI 환경에 원격으로 접속하실 수 있습니다.






---
<p align="center">
© 2020 Amazon Web Services, Inc. 또는 자회사, All rights reserved.
</p>
