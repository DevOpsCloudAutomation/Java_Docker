pipeline
{
    agent any

    tools
    {
        maven 'Maven_3.9.6'
    }

    environment
    {
        buildNumber = "${BUILD_NUMBER}"
    }

    stages
    {
        stage('Git Checkout')
        {
            steps()
            {
                git branch: 'main', url: 'https://github.com/DevOpsCloudAutomation/JavaDockerApplication.git'
            }
        }

        stage('Build Project')
        {
            steps()
            {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Test')
        {
            steps()
            {
                sh 'mvn sonar:sonar'
            }
        }

        stage('Build Docker Image')
        {
            steps()
            {
                sh 'docker build -t devopscloudautomation/webapplication:${buildNumber} .'
            }
        }

        stage('Push Docker Image')
        {
            steps()
            {
                withCredentials([string(credentialsId: 'Docker_Hub_Password', variable: 'Docker_Hub_Password')])
                {
                    sh 'docker login -u devopscloudautomation -p ${Docker_Hub_Password}'
                }
                sh 'docker push devopscloudautomation/webapplication:${buildNumber}'
            }
        }

        stage('Remove Docker Image Locally in Jenkins Server')
        {
            steps()
            {
                sh 'docker rmi -f devopscloudautomation/webapplication:${buildNumber}'
            }
        }

        stage('Deploy Application to Kubernetes Cluster')
        {
            steps()
            {
                echo "Deploy Application to Kubernetes Cluster"
            }
        }
    }
}