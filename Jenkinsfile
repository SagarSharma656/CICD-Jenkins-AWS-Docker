pipeline {
    agent any

    environment {
        CONTAINER_NAME = 'nestjs-app'
        IMAGE_NAME = 'nestjs-app-image'
        EMAIL = 'sagar.237052@gmail.com'
        PORT = '3000'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git (
                    branch: 'main', 
                    url: 'https://github.com/SagarSharma656/CICD-Jenkins-AWS-Docker.git'
                )
            }
        }

        stage ('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage ('Stop and Remove Existing Container') {
            steps {
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage ('Docker Container Run') {
            steps {
                sh '''
                    docker run -d --name $CONTAINER_NAME -p ${PORT}:${PORT} $IMAGE_NAME
                '''
            }
        }

        stage ('Send Email Notification') {
            steps {
                emailext(
                    subject: "NestJs - Jenkins Build Notification ",
                    body: "The Jenkins build and deployment process of NestJs has completed successfully.",
                    to: "${EMAIL}",
                )
            }
        }
        
    }
}