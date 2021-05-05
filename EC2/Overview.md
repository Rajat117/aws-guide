# Intro
A regional Service that provides compute to run your application in the cloud.
---------------------------
#### Permissions Cheat Sheet
---------------------------
- W (Write)- 4
- R (Read) - 2
- E (Execute) - 1
---------------------------
#### UG0
--------------------------
- U - User
- G - Group
- O - Others
--------------------------
> Note: By Default Secret pem file permissions = 644(UGO). We need to change it to 400

## SSH Using Windows (Window < 10)
WIndows < 10 don't have SSH utility. So we have to use `PUTTY` there.
> Note: We need to convert Secret pem file into `PUTTY` format i.e. `PPK`

## SSH Using Windows (Window >= 10)
It does support SSH but `chmod` command does not exist. We will have to use the UI provided by windows to do that (It's strange right, After trying it on UI you will feel, command is so much the better way).

# Troubleshooting EC2 connectivity issue
|    Problem    | Could be Solution |  Reason  |
|:-------------:|:-----------------:|:---------:|
| Connection Timeout  | Secuirty Group Rule    | SG not allowing incoming port |
| Still Connection Timeout | Check for corporate firewall or personal one | - |
| SSH not working | Use PuTTy | You are using windows < 10 |
| Connection refused | Try to Restart Instance | Don't know somwthing wrong at instance level |
| Permission Denied| Wrong SSH Key or No SSH Key | SSH keys prvoided by AWS can access EC2 only|
| Can't connect after restarting instance | Check for new public IP in console | IP Changes after restart|

# Security Groups
A set of constraint we put on incoming & outgoinh traffic of our resources.
## We can have Constraints On
    - Ports
    - IP or IP Ranges (IPv4 or IPv6 - Both)
## Characteristic
- 1 SG ---CanBeUsedFor--> N instances
- 1 Instance --CanHave---> N SG.
- Locked to Region/VPC combination.(Means in another region using same SG id won't work but configuration will)
- One SG can reference another SG (But don't create cycle 1st-SG -Ref-> 2nd-SG -Ref-> 1st Ref).

# IP's
> Note: IPv4 can be used to create 3.7 billion address
## Private
Network not exposed to WWW (public internet - can be used to access resources within that network).
## Public
Network exposed to WWW (Communication happens using public network)
## Elastic IP
It is a public static IP. You can assign to to instances for which u dunn want the IP to change on restart.
- Only 5 Elastic IP in AWS account (Can ask for more by rasing a ticket)
- Avoid using it if possible.

# Set of Commands that can be used to setup Apache
```
Commands to run for setting the web server
sudo su - elevate acess level
yum update -y - update packages with default yes
yum install -y httpd.x86_64 or httpd
systemctl start httpd.service
systemctl enable httpd.service - enabled across reboot
```
> Note: Apache web server html default location - /var/www/html

# EC2 User Data
A script that will run at bootup of your machine. You can place any script you want including setting up a web server like we did before.
> Note: The User Data script will be a [`bash`] or [`shell you have in ami`] script. It runs with the root user (Have root previleges).
> `#!/bin/bash` - Bash script first line

# EC2 Launch Types
- On Demand (Pay on Demand).
  - Highest Cost
  - No need of long term commitment by paying upfront fee.
- Reserved - 
  - All of its categories are reserved for atleat 1 year.
  - Cheaper than On Demand.
  - Categories
    - Reserved - Same as above.
      - Upto 74% dicsount.
    - Convertible - The resouce type can be converted from m to c large type one
      - Upto 54% discount.
    - Scheduled - Running instance on a schedule basis.
      - Upto
- Spot Instances
  - Cheap
  - Short workload ones
  - You can lose instances so less reliable.
  - Upto 90% discount.
- Dedicated Instances
  - Don't wanna share hardware with other customer.
  - No control over instance placement
- Dedicated Host
  - Have an entire physical server for yourself.
  - 3 year period reservation.
  - Costly.
  - Suitable for BYOL (Don't know about it myself).

# ENI
ELastic Network Interface - A virtual network card assigned to your EC2 instances for network managment.
- AZ specific.
## Characteristic
- Can be applied & removed on the fly