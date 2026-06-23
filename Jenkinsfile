pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Pulling code from GitHub'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ameya-nginx:v1 .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop ameya-container || true'
                sh 'docker rm ameya-container || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d --name ameya-container -p 80:80 ameya-nginx:v1'
            }
        }
    }
}
