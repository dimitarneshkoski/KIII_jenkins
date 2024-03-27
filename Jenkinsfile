pipeline {
    agent any
    def app
    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }
        
        stage('Build image') {
            steps {
                script {
                    app = docker.build("dimitarneshkoski/kiii__jenkins")
                }
            }
        }
        
        stage('Push image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        app = docker.image("dimitarneshkoski/kiii__jenkins")
                        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        app.push("${env.BRANCH_NAME}-latest")
                        // signal the orchestrator that there is a new version
                    }
                }
            }
        }
    }
}

