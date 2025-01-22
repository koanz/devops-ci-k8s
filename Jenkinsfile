pipeline {
  agent any
  stages {
    stage('clone repository') {
      steps {
        powershell '''
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
          powershell '''
            kubectl --token %api_token% --server https://127.0.0.1:52916 --insecure-skip-tls-verify=true apply -f deployment-billing-app-back-jenkins.yaml
          '''
        }
      }
    }
  }
}



