pipeline {
    agent any
    tools {nodejs "Nodeauto"}
    environment {
        AWS_REGION = 'us-east-1'
        EC2_INSTANCE_IP = '54.167.123.215'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Hadhemi33/DevOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Install pm2') {
            steps {
                sh 'npm install pm2 -g'
            }
        }

        stage('Deploy Locally') {
            steps {
                sh 'pm2 startOrRestart pm2.config.json'
            }
        }

    }
}
