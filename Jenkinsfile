pipeline {
    agent any

    environment {
        // Set your image name and GitHub repository details
        IMAGE_NAME = 'node-docker-demo'
        GIT_REPO_URL = 'https://github.com/yourusername/your-repo.git'
        GIT_BRANCH = 'master'  
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    git url: "${GIT_REPO_URL}", branch: "${GIT_BRANCH}"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker --version'

                    sh "docker build -t $IMAGE_NAME ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh "docker rm -f $IMAGE_NAME || true"
                    
                    sh "docker run -d -p 3000:3000 --name $IMAGE_NAME $IMAGE_NAME"
                }
            }
        }

        stage('Push Docker Image to Registry') {
            steps {
                script {
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
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
