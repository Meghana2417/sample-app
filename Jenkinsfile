pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "meghana1724/sample-app"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/Meghana2417/sample-app.git'
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
