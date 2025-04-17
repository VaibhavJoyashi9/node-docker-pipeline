pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'nodejs-app:latest'
        DOCKER_REGISTRY = 'root'
        GIT_REPO = 'https://github.com/VaibhavJoyashi9/node-docker-pipeline.git' 
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    git branch: 'main', url: "${GIT_REPO}"
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    bat 'docker build -t ${DOCKER_IMAGE} .'
                }
            }
        }
        stage('Push Docker Image to Registry') {
            steps {
                script {
                    // Log in to Docker Hub (if needed)
                    bat 'echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin'
                    
                    // Tag the image with your Docker Hub registry
                    bat 'docker tag ${DOCKER_IMAGE} ${DOCKER_REGISTRY}/${DOCKER_IMAGE}'

                    // Push the Docker image to Docker Hub
                    bat 'docker push ${DOCKER_REGISTRY}/${DOCKER_IMAGE}'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    bat '''
                        docker pull ${DOCKER_REGISTRY}/${DOCKER_IMAGE}
                        docker stop nodejs-app || echo "No container to stop"
                        docker rm nodejs-app || echo "No container to remove"
                        docker run -d --name nodejs-app -p 80:3000 ${DOCKER_REGISTRY}/${DOCKER_IMAGE}
                    '''
                }
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
