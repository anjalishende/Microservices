pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withCredentials([file(credentialsId: 'k8-token', variable: 'KUBECONFIG')]) {
                    sh '''
                    export KUBECONFIG=$KUBECONFIG
                    kubectl apply -f deployment-service.yml
                    '''
                }
            }
        }

        stage('Verify deployment') {
            steps {
                withCredentials([file(credentialsId: 'k8-token', variable: 'KUBECONFIG')]) {
                    sh '''
                    export KUBECONFIG=$KUBECONFIG
                    kubectl get svc -n webapps
                    '''
                }
            }
        }
    }
}
