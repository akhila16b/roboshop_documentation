# 🛒 Roboshop Documentation

## MongoDB Security Group Setup

### Step 1: Create Security Group
Create a security group named **roboshop-mongodb**.

### Step 2: Configure Inbound Rules

| Type | Source |
|--------|--------|
| SSH (22) | My IP |

### Expected Result
The security group **roboshop-mongodb** is created with SSH access enabled from your current IP address.

## Catalogue setup Security Group Setup

### Step 1: Create Security Group
Create a security group named **roboshop-catalogue**.

### Step 2: Configure Inbound Rules

| Type | Source |
|--------|--------|
| SSH (22) | My IP |

## user Security Group Setup

### Step 1: Create Security Group
Create a security group named **roboshop-user**.

### Step 2: Configure Inbound Rules

| Type | Source |
|--------|--------|
| SSH (22) | My IP |

27017 - roboshop-catalogue   mongodb accepts connections on port no 27017 from the instances with SG attached as roboshop-catalogue.
27017 - roboshop-user        mongodb sccepting connections on port 27017 from the instance where roboshop-user is attached.

## Instance setup for mongodb

### Create an instance named roboshop-mongodb
Without key-value pair and attach SG = roboshop-mongodb
Take care of OS as AMI

Connect to ssh by public ip

Setup the MongoDB repo file 

``` shell title=/etc/yum.repos.d/mongo.repo
[mongodb-org-7.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/9/mongodb-org/7.0/x86_64/
enabled=1
gpgcheck=0
```

Hint! You can create file by using **`vim /etc/yum.repos.d/mongo.repo`**

Install MongoDB 

```shell 
dnf install mongodb-org -y 
```

Start & Enable MongoDB Service 

```shell 
systemctl enable mongod 
systemctl start mongod 
```

Usually MongoDB opens the port only to `localhost(127.0.0.1)`, meaning this service can be accessed by the application that is hosted on this server only. However, we need to access this service to be accessed by another server, So we need to change the config accordingly.

Update listen address from 127.0.0.1 to 0.0.0.0 in `/etc/mongod.conf`

You can edit file by using **`vim /etc/mongod.conf`**

If you want to more precise means as you should access from only catalogue server we can give only that ip but if ip change again issue but in SG level we can restrict.

Restart the service to make the changes effected.
systemctl restart mongod

netstat -lntp
Restart the service to make the changes effected.

```shell 
systemctl restart mongod
```










