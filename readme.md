Abdullah Alaqeel  
G00915482

---

## Server:
![Cluster](cluster.png)
I created a t2.medium EC2 instance and:
* installed docker
* installed jenkins
* ran rancher as a docker container
```
sudo yum update
sudo yum install docker
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -a -G docker ec2-user
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo yum upgrade
sudo yum install jenkins java-1.8.0-openjdk-devel
sudo systemctl daemon-reload
sudo systemctl start jenkins
docker run -d --restart=unless-stopped --name rancher -p 80:80 -p 443:443 --privileged rancher/rancher:latest
```


## Agents:
After much trial and error, I decided to go with setting up RKE on Azure virtual machines. My deployment contains 2 virtual machines deployed automatically by Rancher.   
I used this [tutorual](https://docs.microsoft.com/en-gb/azure/active-directory/develop/howto-create-service-principal-portal) to do the steps necessary to link Rancher with Azure.  

![Deployments](deployments.png)

## Jenkins
I created a multi-step jenkins pipeline and used multiple plugins to achieve the desired goal. The steps I went through are similar to the reference document.

However, to deploy the updates to kubernates, I run a kubectl script to update the image in the kubernates deployment, which is then rolled out to all the pods.

![Jenkins Build Config](JenkinsBuildConfig.png)

---
### Public IP Addresses:
Server:
* Rancher: https://54.86.219.59
* Jenkins: http://54.86.219.59:8080


Agnets (load balanced)
* http://138.91.190.41
* Survey: http://138.91.190.41/survey