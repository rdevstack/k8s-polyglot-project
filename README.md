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
