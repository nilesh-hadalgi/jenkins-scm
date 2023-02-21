# Setting Up Jenkins on EC2 as ec2-user

This guide provides step-by-step instructions for setting up Jenkins on an Amazon Elastic Compute Cloud (EC2) instance running Amazon Linux or Red Hat Enterprise Linux (RHEL) as the ec2-user.

## Prerequisites

- An EC2 instance running Amazon Linux or Red Hat Enterprise Linux (RHEL).
- An SSH client to connect to your instance (e.g., PuTTY, OpenSSH, or Git Bash).
- A key pair to connect to your instance. You can create a key pair in the Amazon EC2 console or using the AWS Command Line Interface (CLI).
- A basic understanding of the Linux command line interface.

## Steps

1. Launch an EC2 instance running Amazon Linux or Red Hat Enterprise Linux (RHEL).
2. Connect to the instance using SSH.

```
ssh -i your-key-pair.pem ec2-user@your-instance-public-dns-name
```
Replace "your-key-pair.pem" with the name of your private key file and "your-instance-public-dns-name" with the public DNS name of your instance.
3. Update the instance to the latest packages.

```
sudo yum update -y
```

4. Install Java on the instance.
```
sudo yum install java-1.8.0-openjdk-devel -y
```
5. Add the Jenkins repository to the instance.
```
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key
```
6. Install Jenkins on the instance.
```
sudo yum install jenkins -y
```
7. Start the Jenkins service.
```
sudo systemctl start jenkins
```
8. Check the status of the Jenkins service.
```
sudo systemctl status jenkins
```
If the service is running, you should see the status as "active (running)".
9. Open the Jenkins web interface in your browser.

```
http://your-instance-public-dns-name:8080
```
Replace "your-instance-public-dns-name" with the public DNS name of your instance.
10. Retrieve the initial admin password and unlock Jenkins.

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Copy the password and paste it into the "Administrator password" field on the "Unlock Jenkins" page.
11. Follow the prompts to complete the Jenkins installation. You will be asked to create an admin user and install any recommended plugins.
12. Enable Jenkins to start automatically on system boot.

```
sudo systemctl enable jenkins
```

## Conclusion

By following these steps, you should now have Jenkins running on an EC2 instance as the ec2-user, and the service should start automatically on system boot. From here, you can configure Jenkins to suit your specific needs and begin using it for continuous integration and delivery workflows.
