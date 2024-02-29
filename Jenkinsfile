pipeline {
    agent any
    
    parameters {
        string(name: 'DOCKER_IMAGE', defaultValue: '', description: 'Name of the Docker image to pull from Docker Hub')
        string(name: 'PORT_MAPPING', defaultValue: '8080:7777', description: 'Port mapping for running the container (e.g., <host_port>:<container_port>)')
    }
    
    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    docker.image(params.DOCKER_IMAGE).pull()
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                script {
                    def dockerCommand = "docker run -d -p ${params.PORT_MAPPING} ${params.DOCKER_IMAGE}"
                    sh label: 'Run Docker Command', script: dockerCommand
                }
            }
        }
    }
}
