
pipeline {
    agent any
environment {
    DOCKER_HOST = 'tcp://host.docker.internal:2375'
}

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-docker-website .'
            }
        }

        stage('Test Website') {
            steps {
                sh 'docker run --rm my-docker-website nginx -t'
            }
        }

        stage('Deploy Website') {
            steps {
                sh 'docker rm -f my-docker-website-container || true'
                sh 'docker run -d --name my-docker-website-container -p 8081:80 my-docker-website'
            }
        }
    }
}

