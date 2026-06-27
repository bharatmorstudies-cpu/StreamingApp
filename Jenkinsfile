pipeline {
    agent any
    environment {
        AWS_ACCOUNT_ID = '775935273911' 
        AWS_DEFAULT_REGION = 'ap-south-1' 
        FRONTEND_ECR_REPO = 'streamingapp-frontend'
        BACKEND_ECR_REPO = 'streamingapp-backend'
        IMAGE_TAG = "${env.BUILD_NUMBER}"
    }
    stages {
        stage('Git Checkout') {
            steps {
                checkout scm
            }
        }
        stage('AWS ECR Authentication') {
            steps {
                script {
                    sh "aws ecr get-login-password --region ${AWS_DEFAULT_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com"
                }
            }
        }
        stage('Build Docker Images') {
            steps {
                script {
                    sh "docker build -t ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}://{FRONTEND_ECR_REPO}:${IMAGE_TAG} ./frontend"
                    sh "docker build -t ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}://{BACKEND_ECR_REPO}:${IMAGE_TAG} ./backend"
                }
            }
        }
        stage('Push Images to Amazon ECR') {
            steps {
                script {
                    sh "docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}://{FRONTEND_ECR_REPO}:${IMAGE_TAG}"
                    sh "docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}://{BACKEND_ECR_REPO}:${IMAGE_TAG}"
                }
            }
        }
    }
}
