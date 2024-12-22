pipeline {
    agent any

    stages {
        stage ('Build Image') {
            steps {
                script {
                    dockerapp = docker.build("fabricionoveronez/api-produto:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }
        stage ('Push image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")  // Aqui, use a interpolação de string
                    }
                }
            }
        }
    }
}
