pipeline {
    agent any

    environment {
        IMAGE_NAME = 'node-docker-demo'
        GIT_REPO_URL = 'https://github.com/VaibhavJoyashi9/node-docker-pipeline.git'
        GIT_BRANCH = 'master'  // Update this if you're using a different branch, like 'master'
    }

    stages {
        stage('Clone Repo') {
            steps {
                script {
                    // Check out the correct branch from GitHub
                    git url: "${GIT_REPO_URL}", branch: "${GIT_BRANCH}"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Check if Docker is installed
                    sh 'docker --version'
                    
                    // Build the Docker image
                    sh "docker build -t $IMAGE_NAME ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove any existing container with the same name
                    sh "docker rm -f $IMAGE_NAME || true"
                    
                    // Run a new container
                    sh "docker run -d -p 3000:3000 --name $IMAGE_NAME $IMAGE_NAME"
                }
            }
        }

        stage('Push Docker Image to Registry') {
            steps {
                script {
                    // Log in to Docker Hub (if needed)
                    // sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"

                    // Optionally, push the image to Docker registry (Uncomment if needed)
                    // sh "docker push $IMAGE_NAME"
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
                    // Clean up old images/containers if needed
                    // sh "docker system prune -f"
                }
            }
        }
    }

    post {
        success {
            echo 'NodeJS App deployed successfully using Docker!'
        }
        failure {
            echo 'Build failed. Check console for errors.'
        }
    }
}
