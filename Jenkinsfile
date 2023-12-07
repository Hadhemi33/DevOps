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

        stage('Deploy to EC2') {
            steps {
                script {
                    // Copy your application to the EC2 instance using SCP or any other method
                    dir("/home/ec2-user/my-app") {
                        sh "scp -i ./nody.pem -o StrictHostKeyChecking=no -r . ec2-user@${EC2_INSTANCE_IP}:/home/ec2-user/my-app"
                    }

                    // SSH into the EC2 instance and execute deployment commands
                    sh "ssh -i ./nody.pem -o StrictHostKeyChecking=no ec2-user@${EC2_INSTANCE_IP} 'cd /home/ec2-user/my-app && npm install && pm2 startOrRestart pm2.config.json'"
                }
            }
        }
    }
}
