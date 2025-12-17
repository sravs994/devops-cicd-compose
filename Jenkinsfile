pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-app"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Set Build Variables') {
            steps {
                script {
                    env.IMAGE_TAG = "${env.BRANCH_NAME}-${env.BUILD_NUMBER}"

                    if (env.BRANCH_NAME == 'main') {
                        env.APP_PORT = '5000'
                    } else if (env.BRANCH_NAME == 'dev') {
                        env.APP_PORT = '5001'
                    } else {
                        env.APP_PORT = '5002'
                    }
                }
            }
        }

        stage('Build Info') {
            steps {
                echo "Branch: ${env.BRANCH_NAME}"
                echo "Build Number: ${env.BUILD_NUMBER}"
                echo "Docker Image: ${env.IMAGE_NAME}:${env.IMAGE_TAG}"
                echo "App Port: ${env.APP_PORT}"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
                '''
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                sh '''
                    export IMAGE_TAG=${IMAGE_TAG}
                    export APP_PORT=${APP_PORT}
                    docker-compose down --remove-orphans || true
                    docker-compose up -d
                '''
            }
        }
    }

    post {
        success {
            echo "Application deployed successfully using Docker Compose"
        }
        failure {
            echo "Deployment failed"
        }
        always {
            echo "Pipeline completed"
        }
    }
}
