pipeline {
    agent any

    environment {
        IMAGE_NAME = "aravind80555/maven_demo"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Aravind162003/maven_demo'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image using Jenkins Docker DSL
                    dockerImage = docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                        dockerImage.push("latest")
                    }
                }
            }
        }
    }
}
