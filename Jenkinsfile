pipeline {
    agent any
    
    parameters {
        string(name: 'DOCKER_IMAGE', defaultValue: '', description: 'Name of the Docker image to pull from Docker Hub')
        string(name: 'PORT_MAPPING', defaultValue: '-p 8080:80', description: 'Port mapping for running the container (e.g., -p <host_port>:<container_port>)')
        booleanParam(name: 'DETACHED_MODE', defaultValue: true, description: 'Run the Docker container in detached mode?')
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
                    def dockerCommand = "docker run ${params.DETACHED_MODE ? '-d' : ''} ${params.PORT_MAPPING} ${params.DOCKER_IMAGE}"
                    sh label: 'Run Docker Command', script: dockerCommand
                }
            }
        }
    }
}
