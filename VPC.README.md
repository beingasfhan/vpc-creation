# 🌐 AWS VPC Setup – DevOps Project

##  Project Overview

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

##  Services Used

* AWS VPC

* Subnets

* Internet Gateway

* NAT Gateway

* Route Tables

* EC2 Instances

* Security Groups

##  Architecture Diagram

![Architecture Diagram](https://2.bp.blogspot.com/-M5mou_8yyl4/XDLK-2xxWtI/AAAAAAAACeI/f4o3_L2PzP0Q8lVqzpAJ4W25GMdQzUOSwCLcBGAs/s1600/sample%20vpc.jpg)
---


##  Components with Screenshots

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

![AWS VPC Architecture](https://miro.medium.com/v2/resize:fit:641/1*DeUfw9fuFGCpKLwZka4UHg.jpeg)### 2️⃣ Public and Private Subnets

| Subnet           | CIDR        | AZ   | Type    |
| ---------------- | ----------- | ---- | ------- |
| Public-Subnet-1  | 10.0.1.0/24 | AZ-1 | Public  |
| Public-Subnet-2  | 10.0.2.0/24 | AZ-2 | Public  |
| Private-Subnet-1 | 10.0.3.0/24 | AZ-1 | Private |
| Private-Subnet-2 | 10.0.4.0/24 | AZ-2 | Private |

![Public and Private Subnets](https://i.stack.imgur.com/plsWk.png)### 3️⃣ Internet Gateway Attachment

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

![Internet Gateway](https://miro.medium.com/v2/resize:fit:1358/1*gftv4LSqU_12kRqNwYISJw.png)
### 4️⃣ Public Route Table Configuration

![Private Route Table](https://cloudiofy.com/wp-content/uploads/2022/08/21-aws-vpc-create-private-route-table-768x794.png)

### 5️⃣ NAT Gateway with Elastic IP
![IP Insights Architecture](https://d2908q01vomqb2.cloudfront.net/5b384ce32d8cdef02bc3a139d4cac0a22bb029e8/2023/07/27/ip-insights-blog-figure-8.png)
### 6️⃣ Private Route Table Configuration
![Private Route Table](https://cloudiofy.com/wp-content/uploads/2022/08/21-aws-vpc-create-private-route-table-768x794.png)
### 7️⃣ Bastion Host in Public Subnet
![Bastion Host](https://www.pikpng.com/pngl/m/94-942816_the-application-host-resides-in-a-private-subnet.png)
### 8️⃣ Application Server in Private Subnet
![Private Server](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAQcAAADACAMAAAA+71YtAAAB+1BMVEX////m8vjp8+azz+Tp8vjQ3+3m9vzd6/Tc5/Hj7uHZ6da01K/y+Pviq6jx+PDjtrXr9Ojz+PHu+ej3+Pn0wLr86Objyszqurjl7vT++/nV2d+11Ofk7OT67OPI4e/EG10AebjuP37D3OxbnjQrdRfe5OLO2dOjls399vL78Oljnsns7vF6s9aFtn+WhMnWWgDsyrSPWe06gSEAZwBXoUy0rdPx/unztrAAdLZXniheMrq5AE3Y49e5qt4VhACpy6S9ycicjMu/u9ePecfR092Pvdvv1cXkmmsdhb6MUe4+V9xHjSjYLGwreQw1Or6dhtOwndvp5fQwjyCwqNGBZ8LHx9qxu7WFkJA5jsPprIPfrIubxd9BafA9ihWSuoLiXo1xPs8iJrZRH7PNwufc1O94tG/K4cZPnkR4Wb+cqrG6wcuToqw+SlZ1gILompPj187j1t95r1lsifQ3Y++Yq/TzlLVMbu58k/KfsPWWY+7Dzfj2q8Sec+3Oufbg0vm0lfEoUeSxvfTqToX3vdLHsfOng+x4OuC5nuzcFmZdbt1MYNvkb5dknE6HXdl2gd6JkuLzytppnFqStYltQsR6pXBKhzvQUYCAg9MXHLXTfZ2dxqenwauBbL2FfbN8mLFBYE9+nYHhjFfbdTHBmX7vwaLagT7qiH/mb2OUwsCD57xNAAAYm0lEQVR4nO1di1/aWL4PD4sKt0OJzmJAxqWNWECu7a122pHhKW21VnygRSp9CLTAqtupM9Ot25k6nZntw6lb+9iZvb2Pdu3M/TPv7yQnkIQkVRpSnQ/fQF6H/M7JN9/zO6+EEEQTTTTRRBNNNNFEE0000USjYW/FaPn9gKyDB++nGC7j7wXu1np46Dnr7znb09Ojq+PgvQlTfTz0jHi9I2cRDwaDkTWkbrq0Rr08eM+CJBAP/laDIeMagVkm49+/ZNTLg9/r9TJ68PtN/ozfkvEbMn6XQ/X0aYW69dDTw/oHB2lwZ1xeg9tgcJhaVE+fVqiTh7MVHhjY3fI/9vl8tI8iaf1wdWobdg47cQBMky28CaHVxwaQf+6sTCy4AMpaMcVMzmHaR+IgcnIyBxMPrWyA6jx8elHIgxJIkkBT9pQINyGEDSK/uHXp0qVbl27dQku0utrFBhCX/yjClziAvCm2lyW4IPKcGN+wAT6VefBzsOzgx3F2ETp1+NSpw/ks4ObhU4cPH75Z/ckXl7669NUXm6urXz/8CuHSbS5EggeMm6cO30RmOCAeMMhjgHN/QfNjfzl2Dta/YQMUBFEXD4bd/BhX1EAPWbM5m7+Zz4bMZjEPlzbv3P76i69X1x9K8fDl2tp3tTyAtZuIAAQxD+f+evcbho2733x7rsKD2nrYFQ+cHhay2YUF5gqeWjhcEOvhzr3RW5dG12+vr6/f+uqWgIfv7l/+4+X73z0Q8XC4kDWHsgvZgtlsbhfx8Je73x/7nuXh3Lff/PDjHtID8FDInjg8trAAFITaDo/xeRj9Kre++sXDL9bvjW5+PXpplM/D+bXvzgMB99fWYH6+ysPCRn5hA3i4CRZBYAt8Hn749tw5zMOxc+fu/riH9LC10N+PcgQgFDphXhjbqP4EeFj/+uvbq+ujo6Pr66ujo6tcyOXz58+vPYDZ+cvfPYaVBzwe8lmGh42FsbGCuV3Ew5Uriz/87ae//XXy2LErd/eSHrZQogEbaLYg5mH0zu2Ho49yd9DaEyEPa18iGoCLB/e/5PGwMWbOF8zAQ76/v39sI8Tn4Qri4fsrV64c+/HusStVHhTalBrq4XoIrtxCoQBMnAiJeHh05+Hq+qN7tx/eWwcaeDw8WLvMyGEN8AAUUeHh6YK5sIH0kM/35yV5+OlvP3z/A2KjwkNcPpUa6mEMRABEjIXM2Y32pws8HpAU1lc3nzxav7e+eU/Iw32Ghi8frz3+bu0Bn4cxJC7goR9EMZYNLWxVY2R5uPvt9z99c/fKXtPDOMoMx4+PHV8Ye95eMIt4WH/y6Mnmk9XVzUdAwz2+HphcsbaG8sV5gR5CjB6ebjDsSvBw5Ye7Pz27u+f0MD4eAhoYjG9tjB/n83DhQg6IuLB6ZzP3EHi4wOPh8v3Ljx+fBzUAGV++5PFw3Py0YC6EEJ6HsqFxAQ8TjH94xnqJ4I+LgqRIofE8YCeNeHjB8RCCmYCHR3dG/3F7M7f58+bmBT4PLz/55OUvv/xy/vHa+U9++TtsVXkYfx4af5Edf74xjiDkIQY8LM5AeXEjh3i4hnn4oHrAhTbwsPWU48E8fvz40+pPEA/rtzefQMm5vnkBwOeBxeW1tb+/vP/yk1+4kKfjL+CzBUaleIidvhJ8dvr06Wswv1bhYY/o4Sl8jxw5AqkGHsYFPIyuP7nw8MnDR1efyPCAcP/l/c94PBS2Qltb48/NTNYo8Hk4PRP86VqS5eH0s4k9pocj45CTX7x48XTL/BToEPBw4R/rmw8fPXoSXEc0XI1wIQIePll7zOfBHNp6+uIIxriAh9M3ksHF0wwPwWDs2d7SAyT2xfOtra3nT5mUC3m4cOHJpsfzj0dXlXj47BMeD0eOvBg/UoWQh9PXTt9APJx+9uwabOwFPVBsr8DWf4jwgusuIMiHP1+9evVnhKsMft7k+hJefibCLziAeCG2t1Xtf7gmxiIO+JA84K6g3mF2YsCs4gDUH5WaTOVSOQAs0OokDiD/XAOCDaBExoZ7nTiApHy5CpBlMBjHHVUfkof9gSYPLJo8sGjywKLJA4tG8WBBE8lMzIzZYYTJUg2qBljkAqQsV34htsoESEVXm44ay43iwUW2WFotJqNJZ4eZscUCE+liJrTeajTZmYBW2HDhAJcFH2PnAlhbZHBiYiKA60IE+wsdzMQ2mQBk1cK3WhMdOqZm3KlBPHCn8H5gh40XJ3IwJ3OxSWZTlTHUmgHpxuULFcAMly4muU2WCFUs11ymRulBasS3hbkKdreRINyEye1C4nQZFJRjh69vAqiIBCIRyBcxtFNqKNXI7LS4WlGwxeVyw5Emg4JyPqgeMgCD3zHiyGS8I5mREf9IxkIYjCMZv791RCrRiKLkJBFZTAYCyWCQyCEfYZRK0IghYxhxjGQyYNQAlv0GE+E2ZcC0O5ORsSyAhnqw+OHEM94MzCGxfkhsi59wt9gdI363XzK1aBgZ5JCMQIbIJYPMhqQe/H50ykAtYxTmbi9hchDAugkilbEsQIN4ICWumt3e4jY6Mm632+DIOFpg6XAQBoPJ4Hab7JLZA07Zl0Q8QANpkuPBXvs7i8voaHWDHZfB4DCYkOUM4Ta43A6XrsUhpTTNyosd3SFkfMfNehYpHnZUElne4U21qj+QqtxJh65aTMyDKvdg1WikUX5SldSiq5YkqzzkgAqingRLWhZAVR4K/Rgh8z/NKgAZ+c8kEXiFeHgVJGLcTlUsA0KN4SH0OYZZsnTbNRj3EVz0ofokkSOTzFIVpWHHZK7sUJuHqRPw/dxMqpiLgxEm1ZNM9XqHfnJnlhvHw1R+LH+d0QNNUjTto+k6zFeAc/FkZCKZnAjiAQBVPDC23DAeNqby+RMnQA+tNE1TtNKdejtA1avzupoVblHcteVG8QC5oj//+YnrZmjzh30+wuej67mfn4Pksep5ngbqIb+RB3xuhnY3M8rgex8apJvY+0EPyEeij1md1rF0f5SKlhvHAy431emHkdSDKv0wjdWDuR3jkNKQ6s6xX/VQNWtRJRdLGlFFD9hyw3lQRw+SRYOalpt6YBf7RA+SVUc1LWumh0oD9NDB3eAQe7RkoYP1kOVMH9yVaaFlrfRw6HPU8oIKxQmrfjfAqZVsrGFXD62YqetjMNuVYb1VYLnxemAJPzSFGqDQBD1xUK9v0wMZVkSIlVmgOYI8D5Jpw3pARj8HiqfAShtri7HMGGVjkLJ8UGC5ATxMTgr0YOF42MifyEOCD1rN2Xyh3dzfng+1m63tqKqRN6NFId++Kx4sHA9gF6rwwEMh329uK+QLWWy50N4Pa4U2c8hcQwXmoUF6mExOJIORiXI1sZweIFdcn8qzPIT6zf2hfH++v6DPhsyhbN6cD/VDc6T2winlC3eFB7C8MQU8tOez/YX+/iyYBqaz5my23wy70Ka2POQmfMAFGomsEsHxcP16forRQ6hwKNsP3i2f7w/pESl5SKsZJV9WD5J+sqqHqfz1E4iHQuhQiDltsNxeCCHLIbCfzWZl9dAQP5lLgiAiwYlFYpIjAo/jIB5QNkY8tIGHaEcTfKzwQfVv2NXWrm+X04PEUAVfD4yDQH4STLN29SCAgp5Za2vTg2U5/2BvBA8xIhfJBZO5xVfEInfHppHjIX8dFIH8JHZhVn3FXWKHKeEpDwlOWQgdxwNreUpv5QxWPvp3+slG1KPg3BcXJyaJxWSAHWEgKuM4h1AzfGqKLS92AcyDZL3axfHAWp6SPF1ZHBRYVpWHJEksBicXSWICeGD7VCvjelwDtFagO+FBUg/YxbXVZ7mBeohMJgGRG0QAeBhkb9bgxvUU6ggIVuEGN3E8SDaxseWDVozqUTUW5XloRLs7Qk7mFieDSWIiQhBBlgeywkMVNoCIhjC6ERYAi7Az3FaZnOiuWMpn8MGMIuO8iSINsA/AHNPGP4Y1Niw6cVGsmIdG9MPAqeeSyUnCF/yvin8g7WIebHR0ejDlFDIhTjSHHehB7sKHBQE1sTZQD5NoADa46IvlggSJ75S3iFNr9URSFBUNTAuICMucDeZBsomN/aSc43XyWXBGxLE2UA/gIMBR5oK5mA+tMuD8JHeezlfxIaRQWyrGT3RbzWlY+TxI6sGuyIOVTy39isKxBkQ8NKTfnowBERMTSR+R5G7us7QKeLDF6BspmqJhLR7gKaJGD84y+keH4XAJDX6QRYpAC6KEnmZBe0pEseT2kSXSR9JtAPitmAg+tRBrnI015bE1Xg8EyQ665WK5yi4LnwdbNGqNvUpNz6AkTcelriNOZrgcLhbLs8ViqUSVymgBIIoEBYtyKV4iykWqVCzGyzArop/2MjHwXGG4ahIcw6tYdHoGsorNQzVeD4gCaGUlF6vD6Nz9UZgHkOW03jbkofVOyLO8RONwK5WKI2dmLYeBBMQFnC6ceLEUL1JFokzG43DOQA1RjP834qdc7C3CZ7Y8jEigUylaLyqLUKw2J4o14oRYaSyIhuqBQ027G/NgjdicMdpm89C26YAtIE6w1ROYjg5GApQNCpBwsa3Y62T+4wRKR1iQkB/QMyS0j6DgQxmZYtPnHB4edvYOt4HmY55oNBiL2kR6cKJYnTZbxGnzRGwBAQ+qlxckv8Owph8G8+D0QIpuTAduBCIzsWik6hQYPdCv4nonQoA5FVQlUiov8E7OT9o8HuZoW1TML0iAjs3gWFMRQb5QWw8g11IZrhJNU0WaCqG/vqFoX5UcfMpwMQKyenjlHJrxeDxQokRSWNxK5YVFwINtcHAoGvB4IoEh1gML9RDAevA0WA++YpGY81GludJSuVT+nzLMl8rlaj9t1T94sH/QczkV68HmidtsgaGhoWjKZnulF/CwAz3QAZttkBoasqFlSuAjbDGb06ORfyiF58JFylecmwMGiv9bLpbm5sJzhEgPUF7oK+UF57k5wIWyxUAPsTj8Dp/JjvVgm6bgKNCDB3lfdM155UU0KlteqN7e9CE/RpZRiU76UHlBkhQl1gMIAuoPTholKB4R1h8oVNej4rFUHH5LeQQ8KI3jHKwoTe+MRyNxRHGAX5lEgqBuxNlYxfUHrcdxKvXJWKU+ydcu8vbgHIdeRaPRQNym58pUpf4HUsgDqCnqQYcPwUWn+XpAtVhcn4xWKm8N7H+Q4kFYXgCswUA0Hh8MDAquGOghPgjuYWZwiJ6ZoSq5eAfjOBU92KIzMeuQZ8YDHpEWVdWdnggbq7h9ofE4Dr+96UxBy09U24FE05Gh1Aw1Q3s8gx59alDAg9I4DuYh4nTGUoEoBSYoW0zUvpCItbH99jU8VP0DM7rCdMTU9j8gEUOmDnhuTHsisUCA5jL4zvUQn055ZuDYwZlpD+NqWD1w4zly/Q8tGvFQ0UNbLzSbemdnh602q83Wa7Oh5KE5kyrUSqIjKU/UE/dMD3qi08L6w7v1AIKIw9HTyATTlGX1wMXaVhOr1nrg/MPwn3pni7PhWWvvHCyXYB6ehWbU7CxDRC86k6iH8WW2oVTFmynxIKpPQoWd8YVDVuRocdfO8J/CENssijUsjFVjHirti+G5pdmlpfCsbW54bnZpbm52bmludnapyPLAJBrKkCjtpFORam/JDsZxqv0PEU/c6aSmoQHDUatnY50No1iLEGsRxQors1r7yaoeZmfn4FqErb2QnLlieK53rtgLdIQrekBt7tR0xBPl9Z7tYBynyoONGvREpuP4aFYPECtki15rGMUK5IMihmHZa23kOI4ED9X2JuRLplu5d7YN1IvyK8qps6w76+VOReTNlPRgFPMg9IWsSYhDLxGr5uWmqD9Kr5cataryIMYOxnHk+ieFJoWxWjWvR4n7J3eU6BoeJOvVyv2TsiYxNK5X1/RXS+Md/fbvrwc5HjTTQ834xbsTXTuepTSud1B0DBeTHLVCHrTql+N4UE6Unjee1SsxntXKjGcJRrQosiQzntXGGgsrx4jvj9LqflpuXO8d97IdQmDnzAo3KfXD4Cpx7THcnp3cL6e1Ht4PSuN6qljWzE++H5TG9VSx3Ph6VHcXTH3dfUf7jsKnj9kkutndTBA/oEs+AAWhXXhCs65u0cQF9EkFHJUK6G7s8zhVs30DHA8AWIiS0Sd1urU8lNBOYv7fMRJMACU+Jy4WidOtGBMHhTXioauvDrM1YHPxNlBw5jXMuplNVZ7PSrCLxushUYfZGrC5GPHw+k2Fh/11v30Xu0B/yYBgsOwKOPtW9PDm7Zs3HA/sTgs2POKoy/KARjxgPZBne3rOes/2fOo16nYDXKxxeng9/+Y15Ay+HnSf9vSgly586q/Lssb99sDDWS96Z4jXUk9qq/6Bly/YnTqg4SJ6C4e/Lsva68Hrvei9CDwYDSN+l8NhMrndGZNLZ3KbTCa/Gy1cIy7Fq8b4ybci/wA8eC9e9F/s8RuNGfRGGjDkNjhcJmzZBQuXyb9n9AC5Al02hocRb8brR/9k4/fqRjKOjN+fQf8S4/ebZFJrrPDwtqoHEvMAckCW/RbjSIa1jOz5Lf5MxuEHuxlkes/o4ezFi16Wh4zb4neMeNHfBPlHdI4RlM6Mn0lyi+JVS5zBOMpscnoAGlCWAz2MmIzsWSNejej/cvxe9N87YHnv6AHyBJosOrjoJgSkV5QvdC6XC0kYNuX0INlI4fwD4x4QDxXLLvTRtbh1EIVL2bL2eoBcfNFfp59UGMcBHpBlb51+UrNxnC7MQ89ZhF3zkIbjt9HzONvbXV1gbDvBLJBdklnae1jLn+6L8oJwcdhVYnW+dGJ7+8zAvwaI9EBifmA7nU6fSQ+k0wSs/Ws+ne6ePzOPDdcof0c8aKYH3L7YXSWHwwE48/n59HY43ZVIpOFzBoiAlTSRTpxJzG+n4Tvvq8v0B9LDgfqwQnQnEt1HP+oiEgPEAFrv7j7anZ4nBl4n3N2JvoFEeqUuwxwPlEY84PZm3/K/1YeTDPCCwzJ8lrmddRpeZtOncXuz8+P69ICvmuRzzbgQqc/wgT+wR9Ma8dB1lONB1gfsIBcrPZ+l4F0UDHM8rGjFw4osDwdWdAndCr1C0+/kQbKf1qXMw4pvhfat6FaUedBcDzUpsdvP0K/p+ZXt7YT9XTwojeNIH2in0yvz2ytpiELSuuZ66MY8iPVwYOX1PIe3sgpW0kOrAg8H0hXj82kp6x+MB3FCVtKJis9Kb8tlDUE/jAhKehh4XfWIbwcUeAhrzYP4otADA9yuA+kVuZyhpAclHugzFYuQ/RR40KrclOPhwMAZHg/pevSg4Cft82+r62/nFXgIa8WDrJ9M8HiQrRpjHiT/AsUuz4NOl+bpQSpcaz30yZSbB7bfVnk4c0amdFPUg1ueB3v6TXXjTVqBh7hGPOB6tUT94b31YJTnQagHpfJC83q1OB3v7x8U9KDbsX/QSg+EnB7ev7zg2h5S2HF5oXG7u9ZPJt67/uBQ4GHH9QeN+2kbUZ9U0gNktUp1UtE/aK6H2sT4mPZFAtoX8j1KSu0LJT2g9kVifjuB2heS1j+YHiSSwrQ3fXW3N0klHpj2JnwgCknsIT3g/oF39j90nuzk+u07O3iRKOrhXZY5HjR+HkeKB8oOKT2gY2cKPJzs6PhouXP5ZOfJX0/+ttzR1fHr8vJJZnO5S5YHO4WZkLG+Z/RwoFgsU0WY4iWqRCnx8HHnr7+e/LWvo2N5ueO3jmViufPXDvgmgI1OOR4OzDEPxhcpqthalCqUOR40fh5Hwj+0lotL5aXSHMyW5Ghg88Xyxx+DHkARHR93dJwkPv7tZCfa0fHbSUKOB12pXFpaWiotzUEke7u8KBXLxXKZWqIgqYo8EPxxvc4usMWuOjoJeR7K5dJceYkCnouKPGg8rifVX63bQa8y5kHp+SyZI3WipUx/tdZ6WP6oLvyhg8FHHRLAO+sz/BEev9BqHIe7T8xeH3xdDFq6JIDD6rSs8X1i5EDfQBee+hJHE92JbvjAylEmgMQBfShgZYUN6oMgkgnsw8fwArApCKCqxvqwMZIJOoqOQcaqsZD4GBQgOEarfnt17vaUvP9BtTfvEBo+n/V+UHoeRxXLmj2f9X5Qej5LFcv75LkDpXE9VSzvk+dQlMZxVLG8T3jY/8/jqPm+JBGk3mhZr+V94if3vx7UKTf36/NZobYKhtsaBTUtN+i9cocqf8vb3tuuAv5vxzvrtNzWGB542B/vS6piT7+3uuHvS6qiqQcWTT2waJQe9sf7s6polB72x/uSqtjTemj4+7Oq2NN6UPpfNZUtN0oPqkCy0aqKHmosN+r93QaLw2IgHRY0uY1uu8vUih5PcxuZXRCMfuBgAlpaTC67KMDCPGwmmTaeVfbJNFhhDjaQBl4ALzouoBqdTjP/sN/Q5IFFkwcWTR5YNHlg0eSBRX08/A6hSrOliSaaaKKJJppoookmmmhCEf8ProSeEL3haR0AAAAASUVORK5CYII=)
### 9️⃣ Security Groups Configuration
![Security Groups](https://miro.medium.com/v2/resize:fit:1400/1*dn1AJ7GI207pGILm11RzcA.png)

---

##  Verification
![SSH Verification](https://doimages.nyc3.cdn.digitaloceanspaces.com/008ArticleImages/ssh-console-digitalocean.png)

---


```

> Add your AWS console screenshots into the **screenshots** folder with the above names.

---

##  Summary

The VPC has been configured with two subnets, a public subnet, and a private subnet. If a subnet's traffic is routed to an Internet gateway, the subnet is known as a public subnet. If a subnet doesn't have a route to the Internet gateway, the subnet is known as a private subnet. Instances launched in a private subnet do not have publicly routable internet addresses either.

Both subnets have a route table associated with them. Instances on the public subnet route internet traffic through the internet gateway. The private subnet routes internet traffic through the NAT device (gateway or instance).

Each instance launched in either subnet has its own security group with inbound and outbound rules, to guarantee access is locked down to specific ports and protocols. For example, private instances on the private subnet allow any outbound traffic but only allow SSH access from the bastion host. As another example, although the NAT device is in the public subnet, it cannot be reached from the internet. It has an inbound rule that only grants instances from the private security group (private instances) access. Note that you might allow SSH access from your personal IP address or specific administrator's as well, or perhaps grant ICMP (ping) access during setup and troubleshooting efforts.

In addition to security groups, the private subnet also has a network access control list (NACL) as an added measure of security. NACL's allow for inbound and outbound rules, specified in priority order. They are set up as implicit allow rules. If none of them are matched, all other traffic is denied. This private subnet NACL in this Lab allowed for SSH inbound traffic from the public subnet only. The outbound rules for the private NACL allowed for HTTP/S access to anywhere. This was proven to work in the Lab by performing operating system updates once the NAT device was in place. The private route table sends the traffic from the instances in the private subnet to the NAT device in the public subnet. The NAT device sends the traffic to the Internet gateway for the VPC. The traffic is attributed to the Elastic IP address of the NAT device.
