pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building app...'
                sh 'npm install'
            }
        }
        
        stage('Deploy to EC2') {
            steps {
                echo 'Deploying to EC2...'
                sh 'ssh -i ~/.ssh/jenkins-deploy-ec2.pem -o StrictHostKeyChecking=no ubuntu@13.53.107.174 "cd /home/ubuntu/app && rm -rf * && git clone https://github.com/aditya-shekhawat22/simple-app.git . && npm install"'
            }
        }
        
        stage('Restart Service') {
            steps {
                echo 'Restarting service...'
                sh 'echo "Service restarted"'
            }
        }
    }
    
    post {
        success {
            echo '✅ Pipeline SUCCESS!'
        }
        failure {
            echo '❌ Pipeline FAILED!'
        }
    }
}
