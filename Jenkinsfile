pipeline {
    agent any
    
    environment {
        AWS_REGISTRY = "775935273911.dkr.ecr.ap-south-1.amazonaws.com"
        AWS_REGION   = "ap-south-1"
    }
    
    stages {
        stage('Fetch Source Code') {
            steps {
                checkout scm
            }
        }
        
        stage('Build & Push Auth Service') {
            steps {
                sh 'cd backend/authService && docker build -t streaming-auth .'
                sh 'aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${AWS_REGISTRY}'
                sh 'docker tag streaming-auth:latest ${AWS_REGISTRY}/submission-user-service:latest'
                sh 'docker push ${AWS_REGISTRY}/submission-user-service:latest'
            }
        }
        
        stage('Build & Push Admin Service') {
            steps {
                sh 'cd backend/adminService && docker build -t streaming-admin .'
                sh 'docker tag streaming-admin:latest ${AWS_REGISTRY}/submission-gateway-service:latest'
                sh 'docker push ${AWS_REGISTRY}/submission-gateway-service:latest'
            }
        }

        stage('Build & Push Chat Service') {
            steps {
                sh 'cd backend/chatService && docker build -t streaming-chat .'
                sh 'docker tag streaming-chat:latest ${AWS_REGISTRY}/submission-order-service:latest'
                sh 'docker push ${AWS_REGISTRY}/submission-order-service:latest'
            }
        }

        stage('Build & Push Streaming Service') {
            steps {
                sh 'cd backend/streamingService && docker build -t streaming-streaming .'
                sh 'docker tag streaming-streaming:latest ${AWS_REGISTRY}/submission-product-service:latest'
                sh 'docker push ${AWS_REGISTRY}/submission-product-service:latest'
            }
        }
    }
}
