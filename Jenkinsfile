pipeline {
    agent any

    environment {
        BUILD_CONFIG = "Release"
        DOCKER_IMAGE = "testdocker"
        DOCKER_TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Restore') {
            steps {
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                sh 'dotnet build -c $BUILD_CONFIG'
            }
        }

        stage('Publish') {
            steps {
                sh 'dotnet publish -c $BUILD_CONFIG -o ./publish'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:$DOCKER_TAG .'
            }
        }
    }

    post {
        success {
            echo "Build success!"
        }
        failure {
            echo "Build failed!"
        }
    }
}
