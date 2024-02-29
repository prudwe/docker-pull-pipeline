pipeline {
    agent any

    parameters {
        string(name: 'DOCKER_IMAGE', defaultValue: '', description: 'Docker image to pull')
        string(name: 'PORT_MAPPING', defaultValue: '', description: 'Port mapping for running the container (hostPort:containerPort)')
        string(name: 'DOCKER_HUB_CREDENTIALS', defaultValue: '', description: 'Docker Hub credentials ID')
    }

    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-credentials', url: 'https://index.docker.io/v1/') {
                        docker.image("${params.DOCKER_IMAGE}").pull()
                    }
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    docker.withRun("-p ${params.PORT_MAPPING}") {
                        docker.image("${params.DOCKER_IMAGE}").run()
                    }
                }
            }
        }
    }
}
