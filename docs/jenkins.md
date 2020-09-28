# 安装jenkins
## docker 部署 jenkins

```shell script
docker run -d --name myjenkins --restart=always -p 8081:8080 -p 50000:50000 -v jenkins-data:/var/jenkins_home  fc277073030/jenkins:latest
```