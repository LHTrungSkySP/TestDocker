pipeline {
    agent any
    environment {
        IMAGE_NAME = "testdocker_multi"
        CONTAINER_NAME = "testdocker_multi"
        PORT_HOST = "2000"
        PORT_CONTAINER = "8080"
        BRANCH_NAME = "dev"
        REPO_URL = "https://github.com/LHTrungSkySP/TestDocker.git"
    }
    stages {
        stage('Checkout branch') {
            steps {
                git(
                    branch: "${BRANCH_NAME}",
                    credentialsId: "${env.GIT_CRED_ID}",
                    url: "${URL}"
                )
            }
            post {
                failure {
                    echo "Checkout project FAILURE"
                }
            }
        }
        stage('Build Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }
        stage('Deploy Container') {
            steps {
                sh '''
                    docker rm -f ${CONTAINER_NAME} || true
                    docker run -d --name ${CONTAINER_NAME} -p ${PORT_HOST}:${PORT_CONTAINER} ${IMAGE_NAME}:latest
                '''
            }
        }
    }
}