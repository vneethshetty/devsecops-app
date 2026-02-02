pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/vneethshetty/devsecops-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devsecops-app .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker rm -f devsecops-app || true'
                sh 'docker run -d --name devsecops-app -p 3000:3000 devsecops-app'
            }
        }
    }
}
