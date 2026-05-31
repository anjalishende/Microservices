pipeline {
    agent any

    stages {

        stage('Deploy to Kubernetes') {
            steps {
                withKubeCredentials([[
                    credentialsId: 'k8-token',
                    serverUrl: 'https://03910DA76983FE3503DBDBA8AC0E381E.gr7.us-east-1.eks.amazonaws.com',
                    namespace: 'webapps'
                ]]) {
                    sh 'kubectl apply -f deployment-service.yml'
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                withKubeCredentials([[
                    credentialsId: 'k8-token',
                    serverUrl: 'https://03910DA76983FE3503DBDBA8AC0E381E.gr7.us-east-1.eks.amazonaws.com',
                    namespace: 'webapps'
                ]]) {
                    sh 'kubectl get pods -n webapps'
                    sh 'kubectl get svc -n webapps'
                }
            }
        }

    }
}
