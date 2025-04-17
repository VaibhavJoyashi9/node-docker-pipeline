pipeline {
    agent any

    environment {
        IMAGE_NAME = 'node-docker-demo'
        IMAGE_TAG = "${BUILD_ID}"  
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/VaibhavJoyashi9/node-docker-pipeline.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker info'

                    sh "docker build -t $IMAGE_NAME:$IMAGE_TAG ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh "docker rm -f $IMAGE_NAME || true"
                    
                    sh "docker run -d -p 3000:3000 --name $IMAGE_NAME $IMAGE_NAME:$IMAGE_TAG"
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

            script {
                sh "docker rm -f $IMAGE_NAME || true"
                sh "docker rmi -f $IMAGE_NAME:$IMAGE_TAG || true"
            }
        }
    }
}
