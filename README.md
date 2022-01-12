# Deploying paloalto on aws

Topology used:
![image](https://user-images.githubusercontent.com/1181741/149010298-b0b868bc-e212-4053-9a15-a23c6309d0b9.png)

#Deploy VPC
- using 10.10.0.0/16
- then create 3 subnets - private, public, mgmt (with IPv4 blocks of: 10.10.10.0/23, 10.10.250.0/24, 10.10.12.0/25 respectively)
- create route tables (2: private and public) - public would need a default route out to the internet via Internet Gateway then associate Public and Management subnets (to remote access to Palo Alto); private to private subnet association - also will later add to default route to route private subnet to firewall IP

#EC2 
- Launch EC2 instance and use on-demand instance on Marketplace (charged hourly*)
      - Launched Bundle 2, EC2 with mgmt subnet
      - create new key pair (will download PEM file), generate a private key (ppk) file from PEM to be able to SSH in
      - from SSH, can 'set mgt-config users admin password' to set new admin password for HTTPS/web login after commit/write
      - Allocate an Elastic IP for the mgmt interface to be accessible from internet 
      - Create NICs for Public/Private Subnets and attach to PA EC2 instance (can be while runnning)
            - Also Disable 'Change Source/Dest. Check' - IP Address of interface itself must be source or dest of packet 
            
