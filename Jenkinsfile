pipeline {
    agent any
    stages {
        stage('Verify Tools') {
            steps {
                bat 'kubectl version --client'
            }
        }
        stage('Deploy billing App') {
            steps {
                withCredentials(bindings: [
                      string(credentialsId: 'kubernete-jenkis-server-account', variable: 'api_token')
                ]) {
                    bat 'kubectl --token %api_token% --server https://192.168.49.2:8443 --insecure-skip-tls-verify=true apply -f deployment-billing-app-back-jenkins.yaml --validate=false'
                }
            }
        }
    }
}




