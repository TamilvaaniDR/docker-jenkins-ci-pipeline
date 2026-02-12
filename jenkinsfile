pipeline {
    agent any

    environment {
        IMAGE_NAME = "kaira-app"
        CONTAINER_NAME = "kaira-container"
        PORT = "8090"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $IMAGE_NAME -f docker/Dockerfile .
                '''
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh '''
                docker run -d -p $PORT:80 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment Successful! App running on port 8090 🚀"
        }
        failure {
            echo "Deployment Failed ❌"
        }
    }
}

