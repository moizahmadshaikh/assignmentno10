pipeline {
    agent any 
    
    environment {
        // Define environment variables if needed
        DOCKER_HUB_CREDENTIALS = '2d9006d0-0231-4b08-9eb2-76832adbff8e'
        DOCKER_IMAGE_NAME = 'moizshaikh/assignment10dockerimage'
        DOCKER_IMAGE_TAG = "${DOCKER_IMAGE_NAME}:${env.BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    def dockerImage = docker.build("${DOCKER_IMAGE_TAG}")

                    // Authenticate with Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', "${DOCKER_HUB_CREDENTIALS}") {
                        // Push the Docker image to Docker Hub
                        dockerImage.push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Docker image built and pushed successfully"
        }
    }
}
