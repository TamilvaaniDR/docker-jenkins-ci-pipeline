pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t kaira-app -f docker/Dockerfile .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop kaira-container || true'
                sh 'docker rm kaira-container || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8080:80 --name kaira-container kaira-app'
            }
        }
    }
}
