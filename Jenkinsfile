pipeline {
    agent any
    stages {
        stage('Checkout branch') {
            steps {
                git(
                    branch: "${params.Branch_Name}",
                    credentialsId: "${env.GIT_CRED_ID}",
                    url: "https://github.com/LHTrungSkySP/TestDocker.git"
                )
            }
            post {
                failure {
                    echo "Checkout project FAILURE"
                }
            }
        }
        stage('Build image') {
            steps {
                sh "docker build -t testdocker:latest ."
            }
        }
        stage('Run container') {
            steps {
                sh 'docker run -d --name testdocker -p 1000:8080 testdocker:latest'
            }
        }
    }
}