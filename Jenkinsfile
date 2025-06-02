pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    docker build -f /home/ec2-user/Jenkins/workspace/Jenkin/Dockerfile -t NetflixClonepage /home/ec2-user/jenkins/workspace/Jenkin
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker run -d -p 82:80 NetflixClonepage
                '''
            }
        }
    }
}