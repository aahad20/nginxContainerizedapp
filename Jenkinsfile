pipeline {
    agent any
    environment {
        IMAGE_NAME = "nginx"
        CONTAINER_NAME = "nginx-container"
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/aahad20/nginxContainerizedapp.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                    sh "timeout 10s docker run -d --name ${CONTAINER_NAME} -p 90:80 ${IMAGE_NAME}"
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                script {
                    sh "sleep 5"
            sh "curl -I http://localhost:90"
            sh "exit 0"
                }
            }
        }
    }
}
