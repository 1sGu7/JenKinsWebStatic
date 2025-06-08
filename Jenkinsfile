pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/1sGu7/JenKinsWebStatic.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image từ thư mục chứa Dockerfile (nếu Dockerfile ở root repo thì không cần tham số thứ hai)
                    def customImage = docker.build("my-profile-web:latest")
                }
            }
        }
        stage('Stop Existing Container') {
            steps {
                script {
                    // Dừng và xóa container cũ nếu có
                    sh 'docker rm -f my-profile-web-container || true'
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    // Chạy container mới, tách tham số rõ ràng
                    docker.image("my-profile-web:latest").run("-d", "-p", "80:80", "--name", "my-profile-web-container")
                }
            }
        }
    }
}
