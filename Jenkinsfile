pipeline {
    agent any

    environment {
        IMAGE_NAME = 'node-docker-demo'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/your-username/your-repo-name.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $IMAGE_NAME ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove if already running
                    sh "docker rm -f $IMAGE_NAME || true"
                    // Run new container
                    sh "docker run -d -p 3000:3000 --name $IMAGE_NAME $IMAGE_NAME"
                }
            }
        }
    }

    post {
        success {
            echo ' NodeJS App deployed successfully using Docker!'
        }
        failure {
            echo 'Build failed. Check console for errors.'
        }
    }
}
