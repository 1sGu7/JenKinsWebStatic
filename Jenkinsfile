pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/1sGu7/JenKinsWebStatic.git', branch: 'main'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t my-image:latest .'
                }
            }
        }
        stage('Stop Existing Container') {
            steps {
                script {
                    sh '''
                        docker ps -q --filter "name=my-container" | xargs -r docker stop || true
                        docker ps -a -q --filter "name=my-container" | xargs -r docker rm || true
                    '''
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run -d -p 8081:80 --name my-container my-image:latest'
                }
            }
        }
    }
}
