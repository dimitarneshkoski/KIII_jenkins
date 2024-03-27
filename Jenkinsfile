pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }
        
        stage('Build image') {
            steps {
                script {
                    def app = docker.build("dimitarneshkoski/kiii__jenkins")
                }
            }
        }
        
        stage('Push image') {
            steps {
                script {
                    def app // Define app variable here
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        app = docker.image("dimitarneshkoski/kiii__jenkins") // Assign value to app here
                        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        app.push("${env.BRANCH_NAME}-latest")
                        // signal the orchestrator that there is a new version
                    }
                }
            }
        }
    }
}
