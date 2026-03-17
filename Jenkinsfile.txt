pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "ritishaa07iiitk/2023bec0014_45"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/anandritishaa07/devops-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE% .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat 'echo %PASS% | docker login -u %USER% --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                bat 'docker push %DOCKER_IMAGE%'
            }
        }
    }
}