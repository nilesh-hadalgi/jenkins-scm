# Installing Jenkins on AWS EC2 Instance
This guide explains how to install Jenkins on an AWS EC2 instance running Amazon Linux. Jenkins is an open-source automation server that can be used to automate building, testing, and deploying software applications.

## Prerequisites
Before you begin, ensure that you have the following:

An AWS EC2 instance running Amazon Linux.
A user account with sudo privileges.
### Installation Steps
Update software packages on your EC2 instance:
```
sudo yum update –y
```
Add the Jenkins repository to your EC2 instance:
```
sudo wget -O /etc/yum.repos.d/jenkins.repo \
https://pkg.jenkins.io/redhat-stable/jenkins.repo
```
Import the Jenkins-CI key file to enable installation from the package:
```
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
```
Upgrade software packages on your EC2 instance:
```
sudo yum upgrade
```
Install Java on your EC2 instance:
```
sudo amazon-linux-extras install java-openjdk11 -y
```
Install Jenkins on your EC2 instance:
```
sudo yum install jenkins -y
```
Enable the Jenkins service to start at boot:
```
sudo systemctl enable jenkins
```
Start the Jenkins service:
```
sudo systemctl start jenkins
```
Check the status of the Jenkins service:
```
sudo systemctl status jenkins
```
## Conclusion
Congratulations! You have successfully installed Jenkins on your AWS EC2 instance. You can now use Jenkins to automate building, testing, and deploying your software applications.