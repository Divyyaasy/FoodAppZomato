pipeline {
    agent any
    environment {
        AWS_ACCOUNT_ID = '949787944889'
        AWS_REGION = 'us-east-1'
        ECR_REPO = 'zomato/restaurant'
    }
    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t zomato-app:latest .'
            }
        }
        stage('Push to ECR') {
            steps {
                sh '''
                    aws ecr get-login-password --region us-east-1 | \
                        docker login --username AWS --password-stdin 949787944889.dkr.ecr.us-east-1.amazonaws.com
                    docker tag zomato-app:latest 949787944889.dkr.ecr.us-east-1.amazonaws.com/zomato/restaurant:latest
                    docker push 949787944889.dkr.ecr.us-east-1.amazonaws.com/zomato/restaurant:latest
                '''
            }
        }
    }
}
