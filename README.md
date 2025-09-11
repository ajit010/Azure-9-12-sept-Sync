# Azure-9-12-sept-Sync

Azure Admin Associate :



# Task 1. Create Azure free-tier account ..


github.com  -- optional 

ssh (22)

rdp (3389)


storage section -- 

smb (445)




# Task 2. Create a Budget in Azure account .

(set  a scope -- "present subscription"

 set budget value -- 500

 alert limits -- 50%, 90% and 100%

 alert email id -- <<your-emai-id>>
)



Free subscription --  200 USD for 30 days


12 months -- effectively 30 days of free-tier

Azure won't charge you under Free subscription

Verfify your Free subs. by receiving a mail ..

FREE TIER -- 

Message -- upgrade to pay-as-you-go >>> never click it



1. Delete each resource after demo lab

2. Resource groups 


windows -- multiple users 
administrator

user1  , user 2


user1 -- i download a couple of videos, visit some websites

user2 -- browsing some wevsites, dwnload images



if my azure account shared by 10 users


user1-rg  --- 2 vm, 1 db, 1 sg

user2-rg -- 1 vm , 1 netwk interface, 1 sg  --- resource groups




user10-rg - 3 vms, 2 db, 1 ntwrk





# Task 4.  Create a WIndows based VM :


-- Name - demp-windows-machine

-- Region - central india

   Zone -- Anything(zone1)

  OS - Windows 2019 datacenter

   Username -- ajit-admin

   pswd -- <<your-pwsd>>

 Ports -- allow rdp, http

 Stoarge Disks -- 127 GB default

 Network - keep default

 Review and Create ...



# Task 5. To ping into ip address of windows VM

-- step 1 - add a new rule in network security group (ICMP)

-- sstep 2 -- disable firewall in remote windows machine


# Task 6. To view data disk in windows file explorer

-- go to disk management, initialize disk 2 and create a new partition by adding / assigning a new character to new volume ,,



# Task 7.  Install IIS web-server on windows-VM and chane the index page ..


-- Install Web Server (IIS) from 'add roles n features'

-- Use public ip to view the homepage from host machine

-- Change the index file using below file content .



index.html

<!DOCTYPE html>
<html>
<head>
  <title>My Node.js App</title>
  <style>
    body { font-family: Arial; text-align: center; margin-top: 50px; }
    h1 { color: green; }
  </style>
</head>
<body>
  <h1>Hello from Node.js running on EC2!</h1>
  <p>This is served over HTTP/HTTPS with Nginx reverse proxy.</p>
</body>
</html>



# Task 8.  Create a linux based VM and SSH into Vm :

OS image -- ubuntu 24.04 x64 gen 2

size - B1s

Use SSH key-pair instead of username/pswd in authentication

keep default -- rest of settings/config

download ssh key-pair file

username -- ubuntu


Open cmd prompt in local system , use this command :

SSH syntax :

ssh -i ajit-key22.pem ubuntu@4.213.17.102


(Replace your key-pair name and your public-ip)


Use commands in linux terminal :

ls
mkdir demo
cd demo
touch file1
cd ..
whoami
cat /etc/os-release

To update the packages and install web-server :

sudo apt update -y

sudo apt install apache2 -y

sudo systemctl status apache2

======================================================================================================



# Task 9 : Create a VMSS (Virtual Machine Scaling Set)

Prerequisites :

(Subscriptions -- Resource providers -- Microsoft.Insights -- Register ...)

1. orchestration - uniform

2. size - b1s

3. os image - ubuntu 22.04

4. scaling mode - autoscaling

    scaling policy - > 70, add one and <40 , decrease one

    mininmum, desired = 2 and max = 4

5. networking - select the interface and enable the public-ip

6. add ports - http(80) ans ssh (22)

7. Under "Advanced section" add user data :



User data script -


#!/bin/bash
sudo apt-get update -y;
sudo apt install apache2 -y;
echo "Hello, welcome from VM: $(hostname)" > /var/www/html/index.html;


8. Rest - keep as default and create

9. visit the ip addresss of both machines of vmss and you will get same msg displayed...

10. SSH into both of machines :

     ssh username@public-ip-vm
    
     sudo apt install stress

     sudo stress --cpu 10 --timeout 900
    
11. after few minutes (10-12 min), look at the cpu utilization and no. of instances in vmss

12. Go to Activity log under VMSS to check the scaling activity based on scaling condition ...

13. Just like CPU utilization, you can add any metric to scaling condition ...

14. You can use vertical scaling to resize the instances too.. (will apply on new instances only) ...




# Task 10: Create a  VPC and 2 subnets

1. Create a VPC of CIDR range : (10.0.0.0/16)
    
2. Create 2 subnets - subnet1 (10.0.1.0/24) and subnet2 (10.0.2.0/24)



# Task 11: Create Public Ip address :

1. Create 3 public ip (lb-ip, vm1-ip and vm2-ip)

2. Use Ipv4 , SKU - standard , ip assgnmnent - static ...



# Task 12: Create 2 VM and Load Balancer:
    
    
1. Create Vm-1 and Vm-2 (ubuntu 24.04)

2. Size- b1s

3. Availibity set - create new and use same in both VMs

4. Networking - select the existing network and default subnet and vm1-1 ip and vm-2 ip respectively

5. Advanced - "User data"

    for vm1 -
    
    
    #!/bin/bash
    sudo apt-get update -y;
    sudo apt install apache2 -y;
    echo "Hello, welcome to 1st VM" | sudo tee /var/www/html/index.html;
    sudo chown www-data:www-data /var/www/htmlindex.html;


    for vm2 -
    
    #!/bin/bash
    sudo apt-get update -y;
    sudo apt install apache2 -y;
    echo "Hello, welcome to 2nd VM" | sudo tee /var/www/html/index.html;
    sudo chown www-data:www-data /var/www/htmlindex.html;


 6. Create both VMs and acess them using their Ips and check if they display correct msg
    
 7. Create a Load balancer 

 8. frontend config - lb-ip
    
    backend pool - select vnet - select both vms
    
    add a lb rule and health prope ...
    
    
 9. save this info and lb will be created ...

 10. Visit the front-end ip of LB to check distribution of traffic among VMs ...



=============================================================================================================













































