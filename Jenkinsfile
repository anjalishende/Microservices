pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred') {
                        sh "/usr/bin/docker build -t saamrajepatil/cartservice:latest ."
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred') {
                        sh "/usr/bin/docker push saamrajepatil/cartservice:latest"
                    }
                }
            }
        }

    }
}
