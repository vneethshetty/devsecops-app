pipeline {
    agent any

    environment {
        AWS_REGION = "ap-south-1"
        ECR_REPO = "416754239581.dkr.ecr.ap-south-1.amazonaws.com/devsecops-app"
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/vneethshetty/devsecops-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devsecops-app .'
                sh 'docker tag devsecops-app:latest $ECR_REPO:latest'
            }
        }

        stage('Login to ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $ECR_REPO
                '''
            }
        }

        stage('Push to ECR') {
            steps {
                sh 'docker push $ECR_REPO:latest'
            }
        }
    }
}
