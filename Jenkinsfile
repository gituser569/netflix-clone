pipeline {
    agent { label 'kool' }

    environment {
        IMAGE_NAME = 'netflixclonepage'
        HOST_PORT = '82'
        CONTAINER_PORT = '80'
        EC2_IP = 'YOUR_EC2_PUBLIC_IP'  // replace this with your real IP or use Jenkins credentials/env variables
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                    docker build -t $IMAGE_NAME .
                """
            }
        }

        stage('Stop Old Container (if running)') {
            steps {
                sh """
                    if [ \$(docker ps -q -f name=$IMAGE_NAME) ]; then
                        docker stop $IMAGE_NAME
                        docker rm $IMAGE_NAME
                    fi
                """
            }
        }

        stage('Run Docker Container') {
            steps {
                sh """
                    docker run -d --name $IMAGE_NAME -p $HOST_PORT:$CONTAINER_PORT $IMAGE_NAME
                """
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! Visit http://$EC2_IP:$HOST_PORT"
        }
        failure {
            echo "❌ Build or deployment failed."
        }
    }
}
