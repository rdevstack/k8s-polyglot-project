This repository contains the source files needed to follow the series [Kubernetes and everything else](https://rinormaloku.com/series/kubernetes-and-everything-else/) or summarized as an article in [Learn Kubernetes in Under 3 Hours: A Detailed Guide to Orchestrating Containers](https://medium.freecodecamp.org/learn-kubernetes-in-under-3-hours-a-detailed-guide-to-orchestrating-containers-114ff420e882)


# Jenkins Installation

### 1. EC2 Instance

Create an EC2 instance in AWS. For this project , t2.xlarge with Amazon Linux Platform is selected

### 2. Installation Steps

1. SSH into EC2
```
ssh -i keypair.pem ec2-user@ip-address
```
2. Choose Jenkins Long Term Support release for installation
```
sudo yum install wget
```
```
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
```
```
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
```
```
sudo yum upgrade
```
```
sudo yum install jenkins java-1.8.0-openjdk-devel
```
```
sudo systemctl daemon-reload
```

3. Start Jenkins
```
sudo systemctl start jenkins
```
4. Enable Jenkins
```
sudo systemctl enable jenkins
```
5. Jenkins Status
```
sudo systemctl status jenkins
```
6. Navigate to Jenkins URL on browser (http://,EC2-Instance-IP:8080)
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
![jenkins1.png](images/jenkins1.png)

7. Create Admin User

![jenkins2.png](images/jenkins2.png)

8. Create additional users
```
Manage Jenkins > Manage Users > Create User
```


# Github Configuration

1. Upload Source Code to repo
2. Create branch develop
3. Make develop branch as the default branch
4. Generate Tokens
```
1. repo - Full Permission
2. admin:repo_hook - Full permissions
3. admin:org_hook - Full permissions
```
5. Add token to Jenkins
```
1. Dashboard>Manage Jenkins> Manage Credentials> Jenkins > Global Credentials (unrestricted) > Add Credentials > Username/pwd
2. Dashboard>Manage Jenkins> Manage Credentials> Jenkins > Global Credentials (unrestricted) > Add Credentials > Secret text > Token
3. Dashboard> manage Jenkins> System Configuration > Add Github Server > Give Credentials as Jenkins-token
```
6. 