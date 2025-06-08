pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/1sGu7/JenKinsWebStatic.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    def dockerImage = docker.build("my-image:latest")
                    // Các bước khác nếu cần, ví dụ: push image
                }
            }
        }
        stage('Stop Existing Container') {
            steps {
                script {
                    sh 'docker stop my-container || true'
                    sh 'docker rm my-container || true'
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    docker.image("my-image:latest").run("-p 8080:80 --name my-container")
                }
            }
        }
    }
}
