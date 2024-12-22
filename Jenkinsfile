pipeline {
    agent any

    stages {
        stage ('Build Image') {
            steps {
                script {
                    dockerapp = docker.build("fabricionoveronez/api-produto", '-f ./src/Dockerfile ./src')
                    
                }
            }
        }
        
    }
}