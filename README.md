# Ultimate_CICD

Installation of Jenkins on EC2 Instance
1. Launch an EC2 instance with Ubuntu 22.04 AMI

Pre-Requisites to Install Jenkins: 
    Java (JDK)

Run the below commands to install Java and Jenkins
    sudo apt update
    sudo apt install openjdk-11-jre

Verify Java is Installed
    java -version


    curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
    sudo apt-get update
    sudo apt-get install jenkins

**Note: ** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.


Login to Jenkins using the below URL:
    http://ec2-instance-public-ip:8080 [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]

Note: If you are not interested in allowing All Traffic to your EC2 instance 1. Delete the inbound traffic rule for your instance 2. Edit the inbound traffic rule to only allow custom TCP port 8080

After you login to Jenkins, - Run the command to copy the Jenkins Admin Password - 
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword - 
Enter the Administrator password

Install the Docker Pipeline plugin in Jenkins:

Wait for the Jenkins to be restarted.
Docker Slave Configuration
Run the below command to Install Docker

    sudo apt update
    sudo apt install docker.io



Grant Jenkins user and Ubuntu user permission to docker deamon.

    sudo su - 
    usermod -aG docker jenkins
    usermod -aG docker ubuntu
    systemctl restart docker


Once you are done with the above steps, it is better to restart Jenkins.
    http://<ec2-instance-public-ip>:8080/restart
