pipeline {
    agent any

    environment {
        IMAGE_NAME = "akshada0105/docker"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Akshada0105/doc.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME:latest .'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([string(credentialsId 'akshada01', variable: 'akshada0105 ')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u akshada0105 (--add ur docker token here--)
                    sh 'docker push akshada0105/docker:latest'
                }
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker run -d -p 80:80 $IMAGE_NAME:latest'
            }
        }
    }
}
