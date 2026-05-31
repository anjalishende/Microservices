pipeline {
    agent any

    environment {
        DOCKER = "/usr/bin/docker"
        IMAGE = "anjalishende/loadgenerator:latest"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                // 👉 If Dockerfile is in src, keep dir('src')
                // 👉 Else remove dir('src')
                dir('src') {
                    sh "${DOCKER} build -t ${IMAGE} ."
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-cred',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh """
                    echo \$DOCKER_PASS | ${DOCKER} login -u \$DOCKER_USER --password-stdin
                    """
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh "${DOCKER} push ${IMAGE}"
            }
        }
    }
}
