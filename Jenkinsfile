pipeline {
    agent { label 'kool' }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/gituser569/netflix-clone.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t netflix-clone .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker rm -f netflix-clone-container || true
                    docker run -d --name netflix-clone-container -p 8888:80 netflix-clone
                '''
            }
        }
    }
}
