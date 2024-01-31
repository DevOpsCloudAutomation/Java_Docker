
# End to End CICD Pipeline Project

This project can be used to build an end to end CICD Pipeline.
## This project can be used to build multiple CICD Pipeline stages as mentioned below 

- Checkout Code from GitHub.
- Build Project.
- Execute SonarQube Test.
- Build Docker Image.
- Push Docker Image to Registry.
- Remove Docker Image Locally in Jenkins.
- Update Docker Image Tag in Kubernetes Manifest.
- Deploy Application into Kubernetes Cluster.

### Tools and Technologies used are Java, Git, GitHub, Maven, SonarQube, Jenkins, Docker, DockerHub and Kubernetes.

![CICD](https://github.com/DevOpsCloudAutomation/Java_Docker/assets/123757746/085ef572-bd9d-4d05-b710-4fc2a0646d39)
  
# Project Execution
## Build Project

Build Automation Tool Maven can be used to build this project as this project is developed using Java Programming Language.

```bash
  mvn clean package
```
Note:  
Java and Maven should be installed as a prerequisite to Build Project Code.

## Execute SonarQube Test
```bash
  mvn sonar:sonar
```

## Build Docker Image
```bash
  docker build -t devopscloudautomation/webapplication:${buildNumber} .
```

## Push Docker Image to Registry
```bash
  docker login -u devopscloudautomation -p ${Docker_Hub_Password}
  docker push devopscloudautomation/webapplication:${buildNumber}
```

## Remove Docker Image Locally in Jenkins Server
```bash
  docker rmi -f devopscloudautomation/webapplication:${buildNumber}
```

## Update Docker Image Tag in Kubernetes Manifest
```bash
  sed -i 's/Build_Tag/${Build_Number}/g' Deployment.yaml
```

## Deploy Application to Kubernetes Cluster
```bash
  kubectl apply -f Deployment.yaml
```