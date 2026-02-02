pipeline {
    agent any
    environment {
        AWS_REGION = "ap-south-1"
        AWS_ACCOUNT_ID = "YOUR_ACCOUNT_ID"
        ECR_REPO = "devsecops-app"
    }
    stages {
        stage('Build Docker Image') {
            steps { sh 'docker build -t $ECR_REPO .' }
        }
        stage('Login to ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region $AWS_REGION | \
                docker login --username AWS --password-stdin \
                $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com
                '''
            }
        }
        stage('Push to ECR') {
            steps {
                sh '''
                docker tag $ECR_REPO:latest \
                $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$ECR_REPO:latest

                docker push $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$ECR_REPO:latest
                '''
            }
        }
    }
}
