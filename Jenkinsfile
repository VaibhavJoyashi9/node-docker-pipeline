

 pipeline {
    agent any

    environment {
        IMAGE_NAME = 'node-docker-demo'
        GIT_REPO_URL = 'https://github.com/VaibhavJoyashi9/node-docker-pipeline.git''
        GIT_BRANCH = 'master'  // Change to 'master' if your project is on the master branch
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    // Clone the repository from GitHub
                    git url: "${GIT_REPO_URL}", branch: "${GIT_BRANCH}"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Ensure Docker is installed
                    sh 'docker --version'

                    // Build the Docker image using the Dockerfile in the repo
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove any existing container with the same name
                    sh "docker rm -f ${IMAGE_NAME} || true"
                    
                    // Run the Docker container with the built image
                    sh "docker run -d -p 3000:3000 --name ${IMAGE_NAME} ${IMAGE_NAME}"
                }
            }
        }

        stage('Push Docker Image to Registry') {
            steps {
                script {
                    // Log in to Docker Hub (if needed)
                    // Uncomment the next line if you want to push to Docker Hub
                    // sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"

                    // Optionally, push the image to Docker registry (Uncomment if needed)
                    // sh "docker push ${IMAGE_NAME}"
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
                    // Clean up old images and containers if needed
                    // sh "docker system prune -f"
                }
            }
        }
    }

    post {
        success {
            echo 'Node.js application deployed successfully using Docker!'
        }
        failure {
            echo 'Build failed. Check the console for errors.'
        }
    }
}
