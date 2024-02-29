pipeline {
    agent any
    
    parameters {
        string(name: 'DOCKER_IMAGE_NAME', description: 'Enter the Docker image name (format: username/image_name)', defaultValue: '')
    }
    
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-credentials')
    }
    
    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-credentials', url: 'https://index.docker.io/v1/') {
                        docker.image(params.DOCKER_IMAGE_NAME).pull()
                    }
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                script {
                    docker.run(params.DOCKER_IMAGE_NAME)
                }
            }
        }
    }
}
