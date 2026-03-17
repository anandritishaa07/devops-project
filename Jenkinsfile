pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "ritishaa07iiitk/2023bec0014_45"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/anandritishaa07/devops-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $DOCKER_IMAGE'
            }
        }
    }
}