pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = 'nginxweb1'
        CONTAINER_NAME = 'my-docker-container'
        IP_ADDRESS = '172.17.0.3'
        PORT = '80'
        workspace = "172.17.0.2:8080/job/nginxweb1/ws/
    }
    stages {
        stage('Change to workspace directory') {
            steps {
                    dir("${workspace}") {
                    sh "ls -al"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE_NAME} ."
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    sh "docker run -d -p ${IP_ADDRESS}:${PORT}:${PORT} --name ${CONTAINER_NAME} ${DOCKER_IMAGE_NAME}"
                }
            }
        }
    }
}
