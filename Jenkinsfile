pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "shreyas282001/project"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/shreyas282001/project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:latest .'
            }
        }

        stage('Push Image') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub', url: '']) {
                    sh 'docker push $DOCKER_IMAGE:latest'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }
    }
}
