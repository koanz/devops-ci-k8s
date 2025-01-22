pipeline {
  agent any
  stages {
    stage('clone repository') {
      steps {
        bat '''
          java -version
          mvn --version
          git --version
        '''
      }
    }

    stage('Deploy billing App') {
      steps {
        withCredentials(bindings: [
          string(credentialsId: 'kubernete-jenkis-server-account', variable: 'api_token')
        ]) {
          bat '''
            kubectl --token %api_token% --server https://192.168.49.2:50210 --insecure-skip-tls-verify=true apply -f deployment-billing-app-back-jenkins.yaml
          '''
        }
      }
    }
  }
}



