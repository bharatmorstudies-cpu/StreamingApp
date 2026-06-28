pipeline {
    agent any
    
    stages {
        stage('1. Code Checkout') {
            steps {
                // This pulls your latest working code from GitHub into Jenkins
                checkout scm
            }
        }
        
        stage('2. Build Frontend Container') {
            steps {
                echo 'Compiling React and building high-performance Nginx container...'
                sh 'cd frontend && docker build -t streaming-frontend:latest .'
            }
        }
        
        stage('3. Build Backend Microservices') {
            steps {
                echo 'Compiling Node.js environment layers for all microservices...'
                sh 'cd backend/authService && docker build -t streaming-auth:latest .'
                sh 'cd backend/adminService && docker build -t streaming-admin:latest .'
                sh 'cd backend/chatService && docker build -t streaming-chat:latest .'
                sh 'cd backend/streamingService && docker build -t streaming-streaming:latest .'
            }
        }
    }
}
