pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    // Ensure you're using a valid git URL and branch
                    git url: 'https://github.com/VaibhavJoyashi9/node-docker-pipeline.git', branch: 'master'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Ensure Docker is available
                    sh 'docker --version'

                    // Build the Docker image
                    sh 'docker build -t node-docker-demo .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop any running containers with the same name
                    sh 'docker rm -f node-docker-demo || true'

                    // Run the new container
                    sh 'docker run -d -p 3000:3000 --name node-docker-demo node-docker-demo'
                }
            }
        }

        stage('Push Docker Image to Registry') {
            steps {
                script {
                    // Push to Docker Hub (if required)
                    // sh 'docker push node-docker-demo'
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
                    // Clean up unused images
                    // sh 'docker system prune -f'
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
