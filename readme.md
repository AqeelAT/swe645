## Server:
- sudo yum update
- sudo yum install docker
- sudo systemctl enable docker
- sudo systemctl start docker
- sudo usermod -a -G docker ec2-user
- sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
- sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
- sudo yum upgrade
- sudo yum install jenkins java-1.8.0-openjdk-devel
- sudo systemctl daemon-reload
- sudo systemctl start jenkins
- docker run -d --restart=unless-stopped --name rancher -p 80:80 -p 443:443 --privileged rancher/rancher:latest


## Agent:
After much trial and error, I decided to go with setting up RKE on Azure virtual machines.
I used (this tutorual)[https://docs.microsoft.com/en-gb/azure/active-directory/develop/howto-create-service-principal-portal] 
