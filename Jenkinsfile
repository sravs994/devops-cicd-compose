pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-app"
        IMAGE_TAG  = "${env.BRANCH_NAME}-${env.BUILD_NUMBER}"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Info') {
            steps {
                echo "Branch: ${env.BRANCH_NAME}"
                echo "Build Number: ${env.BUILD_NUMBER}"
                echo "Docker Image: ${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
                '''
            }
        }

    }

    post {
        success {
            echo "Docker image built successfully: ${IMAGE_NAME}:${IMAGE_TAG}"
        }
        failure {
            echo "Docker build failed"
        }
        always {
            echo "Pipeline completed"
        }
    }
}
