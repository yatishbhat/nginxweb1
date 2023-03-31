pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = 'yathishbhat/nginxwebcustom'
        IP_ADDRESS = '127.0.0.1'
        PORT = '50'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE_NAME} ."
                   
                   
                }
            }
        }
        stage('Artifact') {
            steps {
                script {
                      docker.withRegistry('https://index.docker.io/v1/', 'my-registry-credentials') {

                 
                         docker.image("${DOCKER_IMAGE_NAME}").push()
                        
                      }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh "docker pull ${DOCKER_IMAGE_NAME}"
                    sh "docker run -d -P -p ${IP_ADDRESS}:8000-8009:80 ${DOCKER_IMAGE_NAME}"
                }
            }
        }
    }
}
