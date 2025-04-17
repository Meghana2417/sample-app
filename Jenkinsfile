pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "your-dockerhub-username/ci-cd-demo"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/your-username/ci-cd-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build(env.DOCKER_IMAGE)
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-creds', url: '']) {
                    dockerImage.push("latest")
                }
            }
        }

        stage('Deploy to K8s') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl apply -f k8s/service.yaml'
            }
        }
    }
}
