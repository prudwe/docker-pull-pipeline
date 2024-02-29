pipeline {
    agent any
    
    parameters {
        string(name: 'DOCKER_IMAGE_NAME', defaultValue: '', description: 'Docker image name')
        string(name: 'HOST_PORT', defaultValue: '', description: 'Host port to map to container port')
        string(name: 'CONTAINER_PORT', defaultValue: '', description: 'Container port to expose')
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
                    def hostPort = params.HOST_PORT
                    def containerPort = params.CONTAINER_PORT
                    
                    docker.withRun("-p ${hostPort}:${containerPort} ${params.DOCKER_IMAGE_NAME}:latest") {
                        // Additional commands to run inside the container (if needed)
                    }
                }
            }
        }
    }
}
