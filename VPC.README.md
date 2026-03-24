# 🌐 AWS VPC Setup – DevOps Project

## 📌 Project Overview

This project demonstrates how to design and configure a secure and highly available **Virtual Private Cloud (VPC)** in AWS with visual references for every component.

---
## Learning Objectives
 Upon completion of this project we will be able to create, configure and test the following:

* Virtual Private Cloud (VPC)
* Internet Gateway
* Public and private subnets (inbound/outbound rules)
* Security groups (inbound/outbound rules for multiple purposes)
* Network access control lists (NACLs) for additional security on a private subnet
* Bastion host for SSH access from the internet to private instances
* Network Address Translation (NAT) Gateway to provide private instances access to the public internet to perform operating system updates
* Route tables associated with public and private subnets

## 🛠️ Services Used

* AWS VPC

* Subnets

* Internet Gateway

* NAT Gateway

* Route Tables

* EC2 Instances

* Security Groups

## 🧱 Architecture Diagram

https://in.images.search.yahoo.com/images/view;_ylt=Awrx.TtpXIxpJIUC_Yy9HAx.;_ylu=c2VjA3NyBHNsawNpbWcEb2lkAzRhZmJmMzY3Y2YyZTMyMmI2OTZiYjEyNWZkOTU3NzNjBGdwb3MDNARpdANiaW5n?back=https%3A%2F%2Fin.images.search.yahoo.com%2Fsearch%2Fimages%3Fp%3Dvpc%2Bcreation%2Bimages%26type%3DE210IN1589G0%26fr%3Dmcafee%26fr2%3Dpiv-web%26tab%3Dorganic%26ri%3D4&w=960&h=720&imgurl=2.bp.blogspot.com%2F-M5mou_8yyl4%2FXDLK-2xxWtI%2FAAAAAAAACeI%2Ff4o3_L2PzP0Q8lVqzpAJ4W25GMdQzUOSwCLcBGAs%2Fs1600%2Fsample%2Bvpc.jpg&rurl=https%3A%2F%2Fwww.learnitguide.net%2F2019%2F01%2Faws-vpc-create-route-tables.html&size=64KB&p=vpc+creation+images&oid=4afbf367cf2e322b696bb125fd95773c&fr2=piv-web&fr=mcafee&tt=AWS+VPC+-+Create+Route+Tables+and+Assign+Subnets+in+AWS&b=0&ni=21&no=4&ts=&tab=organic&sigr=SGA_c3ONZJoN&sigb=sjHiODmA6oZQ&sigi=u_OeXIUYgSkc&sigt=Kt.G7AnDT8OF&.crumb=RNc7FW4NYpa&fr=mcafee&fr2=piv-web&type=E210IN1589G0

---


## 🛠️ Components with Screenshots

### 1️⃣ VPC Creation
Amazon Virtual Private Cloud (Amazon VPC) enables you to launch AWS resources into a virtual network you have defined.

* In the AWS Management Console search bar, enter VPC, and click the VPC result under Services.
* Click Your VPCs in the left navigation pane.
* Click Create VPC to begin creating a new VPC. A Create VPC dialog box is opened for you. Specify the following VPC details:
* Resources to create: Select VPC only
* Name tag: Enter VPC-project
* CIDR block: Enter 10.0.0.0/16
* Tenancy: Select Default
*Scroll to the bottom of the page and click Create VPC.

In this step, we created the non-default VPC that will be configured with private and public subnets.

https://in.images.search.yahoo.com/images/view;_ylt=Awrx.TtcXYxpa8gAA9u9HAx.;_ylu=c2VjA3NyBHNsawNpbWcEb2lkAzMyNzdkMzMzYjI1MWRlNjdkODNlN2EyYjQ5ZThjMWI5BGdwb3MDMTcEaXQDYmluZw--?back=https%3A%2F%2Fin.images.search.yahoo.com%2Fsearch%2Fimages%3Fp%3Dvpc%2Bcreation%2Baws%2Bimage%26ei%3DUTF-8%26type%3DE210IN1589G0%26fr%3Dmcafee%26fr2%3Dp%253As%252Cv%253Ai%252Cm%253Asb-top%26tab%3Dorganic%26ri%3D17&w=641&h=393&imgurl=miro.medium.com%2Fv2%2Fresize%3Afit%3A641%2F1%2ADeUfw9fuFGCpKLwZka4UHg.jpeg&rurl=https%3A%2F%2Fawstip.com%2Faws-custom-vpc-2f07bf8b1537&size=17KB&p=vpc+creation+aws+image&oid=3277d333b251de67d83e7a2b49e8c1b9&fr2=p%3As%2Cv%3Ai%2Cm%3Asb-top&fr=mcafee&tt=AWS+Custom+VPC.+I+wanted+to+launch+%26+connect+my+EC2%E2%80%A6+%7C+by+Naveen+Singh+...&b=0&ni=160&no=17&ts=&tab=organic&sigr=MBwY7ofKZsBc&sigb=H9JWTHBMnjHg&sigi=MeWDsNJZkYrJ&sigt=9MdkhmSSjpy7&.crumb=RNc7FW4NYpa&fr=mcafee&fr2=p%3As%2Cv%3Ai%2Cm%3Asb-top&type=E210IN1589G0

### 2️⃣ Public and Private Subnets

| Subnet           | CIDR        | AZ   | Type    |
| ---------------- | ----------- | ---- | ------- |
| Public-Subnet-1  | 10.0.1.0/24 | AZ-1 | Public  |
| Public-Subnet-2  | 10.0.2.0/24 | AZ-2 | Public  |
| Private-Subnet-1 | 10.0.3.0/24 | AZ-1 | Private |
| Private-Subnet-2 | 10.0.4.0/24 | AZ-2 | Private |

https://in.images.search.yahoo.com/images/view;_ylt=Awr1SY7eXYxpHmcCAwa9HAx.;_ylu=c2VjA3NyBHNsawNpbWcEb2lkAzQ4YTVjYzJlYzRiNDQwZTA3ZWIwNjQ2N2Q5ZjA1MWVjBGdwb3MDMjMEaXQDYmluZw--?back=https%3A%2F%2Fin.images.search.yahoo.com%2Fsearch%2Fimages%3Fp%3Dsubnet%2Bimages%2Baws%26ei%3DUTF-8%26y%3DSearch%26type%3DE210IN1589G0%26fr%3Dmcafee%26fr2%3Dp%253As%252Cv%253Ai%252Cm%253Asb-top%26tab%3Dorganic%26ri%3D23&w=1098&h=528&imgurl=i.stack.imgur.com%2FplsWk.png&rurl=https%3A%2F%2Fstackoverflow.com%2Fquestions%2F45164355%2Fwhat-is-vpc-subnet-in-aws&size=241KB&p=subnet+images+aws&oid=48a5cc2ec4b440e07eb06467d9f051ec&fr2=p%3As%2Cv%3Ai%2Cm%3Asb-top&fr=mcafee&tt=amazon+web+services+-+What+is+VPC%2C+Subnet+in+AWS+-+Stack+Overflow&b=0&ni=160&no=23&ts=&tab=organic&sigr=2vNQf2.dVOQG&sigb=CtPKgCbTr00R&sigi=JC12re56zNrv&sigt=EnmDDnZz3PRJ&.crumb=RNc7FW4NYpa&fr=mcafee&fr2=p%3As%2Cv%3Ai%2Cm%3Asb-top&type=E210IN1589G0
### 3️⃣ Internet Gateway Attachment

* An Internet Gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the Internet.
  * From the VPC Dashboard, click Internet Gateways in the left navigation pane.

  * Click Create internet gateway to begin creating a new gateway with the following:

* Name tag: Enter demo-gw
  * Click Create Internet Gateway:

The State of your Internet Gateway will be detached to start. Now you need to attach the new gateway to the VPC you created earlier.
 * Click Actions then Attach to VPC:

In the Attach to VPC form, select the VPC-project VPC from the drop-down menu.

note: An Internet Gateway can only be attached to one VPC. Therefore, even if you have another Internet Gateway, and it's already attached to the default VPC, the drop-down menu when attaching your Internet Gateway will only include the detached VPC.

* Click Attach internet gateway.
* In the Details tab, you will notice the new Internet Gateway is Attached and available to be used by EC2 instances of the attached VPC.
In this step, we created an Internet Gateway and attached it to the VPC that we created earlier. Instances in the public subnet will route traffic destined for the public internet through the internet gateway.C

https://in.images.search.yahoo.com/images/view;_ylt=Awr1SY67XIxp3kgAcmW9HAx.;_ylu=c2VjA3NyBHNsawNpbWcEb2lkAzM4NWNkM2RiNTBmNzU5NDFmYjY4OTUyZmNmMTNlMzlkBGdwb3MDMQRpdANiaW5n?back=https%3A%2F%2Fin.images.search.yahoo.com%2Fsearch%2Fimages%3Fp%3Dinternet%2Bgateway%2Bimages%2Baws%26ei%3DUTF-8%26type%3DE210IN1589G0%26fr%3Dmcafee%26fr2%3Dp%253As%252Cv%253Ai%252Cm%253Asb-top%26tab%3Dorganic%26ri%3D1&w=1222&h=962&imgurl=miro.medium.com%2Fv2%2Fresize%3Afit%3A1358%2F1%2Agftv4LSqU_12kRqNwYISJw.png&rurl=https%3A%2F%2Fmedium.com%2Fawesome-cloud%2Faws-transit-gateway-overview-9990fd0aaebb&size=82KB&p=internet+gateway+images+aws&oid=385cd3db50f75941fb68952fcf13e39d&fr2=p%3As%2Cv%3Ai%2Cm%3Asb-top&fr=mcafee&tt=AWS+%E2%80%94+Transit+Gateway+Overview.+Introduction+to+AWS+Transit+Gateway+...&b=0&ni=160&no=1&ts=&tab=organic&sigr=_5.iQbXAwCn7&sigb=X7gn2UGUqDho&sigi=NfNcWazPYbVj&sigt=eV84_WqdPLEy&.crumb=RNc7FW4NYpa&fr=mcafee&fr2=p%3As%2Cv%3Ai%2Cm%3Asb-top&type=E210IN1589G0


### 4️⃣ Public Route Table Configuration

https://cloudiofy.com/wp-content/uploads/2022/08/21-aws-vpc-create-private-route-table-768x794.png
### 5️⃣ NAT Gateway with Elastic IP
https://d2908q01vomqb2.cloudfront.net/5b384ce32d8cdef02bc3a139d4cac0a22bb029e8/2023/07/27/ip-insights-blog-figure-8.png
### 6️⃣ Private Route Table Configuration
![Private Route Table](screenshots/private-route-table.png)

### 7️⃣ Bastion Host in Public Subnet
![Bastion Host](screenshots/bastion-host.png)

### 8️⃣ Application Server in Private Subnet
![Private Server](screenshots/private-server.png)

### 9️⃣ Security Groups Configuration
![Security Groups](screenshots/security-groups.png)

---

## 🚀 Verification
![SSH Verification](screenshots/ssh-verification.png)

---

## 📁 Project Structure

```
vpc-project/
 ├── README.md
 └── screenshots/
      ├── architecture.png
      ├── vpc.png
      ├── subnets.png
      ├── igw.png
      ├── public-route-table.png
      ├── nat-gateway.png
      ├── private-route-table.png
      ├── bastion-host.png
      ├── private-server.png
      ├── security-groups.png
      └── ssh-verification.png
```

> Add your AWS console screenshots into the **screenshots** folder with the above names.

---

## 🏁 Conclusion

This repository now includes visual proof of each AWS VPC component, useful for interviews and GitHub portfolio demonstration.
