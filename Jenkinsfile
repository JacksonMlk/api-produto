pipeline {
    agent any

    stages {
        stage ('Build Image') {
            steps {
                script {
                    dockerapp = docker.build("segurox/api-produto:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }
        stage ('Push image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }
        stage ('Deploy Kubernetes') {
            steps {
                script {
                    // Configura o kubeconfig para minikube
                    sh 'kubectl config use-context minikube'
                    // Aplica o deployment no Minikube
                    sh 'kubectl apply -f ./k8s/deployment.yaml'
                }
            }
        }
    }
}
