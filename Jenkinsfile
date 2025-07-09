pipeline {
    agent any

    environment {
        IMAGE_NAME = "739275480317.dkr.ecr.ap-south-1.amazonaws.com/rizwanrepo:latest"
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/main']],
                          userRemoteConfigs: [[
                              url: 'https://github.com/Riz1402/jenkins_pipeline.git'
                          ]]
                ])
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }
        stage('Login to ECR') {
            steps {
                script {
                    sh "aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 739275480317.dkr.ecr.ap-south-1.amazonaws.com"
                    
                }
            }
        }
        stage('Push to ECR') {
            steps {
                script {
                    sh "docker push ${IMAGE_NAME}"
                }
            }
        }
        stage('Create a container') {
            steps {
                script {
                    sh "docker run -itd ${IMAGE_NAME} "
                }
            }
        }
    }
}    