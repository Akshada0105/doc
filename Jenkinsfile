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
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', 
                                                 usernameVariable: 'DOCKER_USER', 
                                                 passwordVariable: 'DOCKER_PASSWORD')]) {
                    script {
                        sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USER --password-stdin'
                        sh 'docker tag $IMAGE_NAME:latest $DOCKER_USER/docker:latest'
                        sh 'docker push $DOCKER_USER/docker:latest'
                    }
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

