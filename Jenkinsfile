pipeline {
    agent any

    environment {
        IMAGE_NAME = "tourism-website"
        CONTAINER_NAME = "tourism-container"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo 'Fetching source code from GitHub...'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Existing Container') {
            steps {
                echo 'Stopping old container if running...'
                sh 'docker stop $CONTAINER_NAME || true'
                sh 'docker rm $CONTAINER_NAME || true'
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running new Docker container...'
                sh 'docker run -d -p 80:80 --name $CONTAINER_NAME $IMAGE_NAME'
            }
        }

        stage('Verify Deployment') {
            steps {
                echo 'Checking running containers...'
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo 'Tourism Website deployed successfully using Docker!'
        }

        failure {
            echo 'Deployment failed. Check Jenkins console logs.'
        }
    }
}
