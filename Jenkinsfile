pipeline {
  agent any
  stages {
    stage('clone repository') {
      steps {
        powershell '''
          java -version 2>&1
          mvn --version 2>&1
          git --version 2>&1
        '''
      }
    }

    stage('Deploy billing App') {
      steps {
        withCredentials(bindings: [
          string(credentialsId: 'kubernete-jenkis-server-account', variable: 'api_token')
        ]) {
          powershell '''
            $ErrorActionPreference = "Stop"
            kubectl --token $env:api_token --server=https://192.168.49.2:49448 --insecure-skip-tls-verify=true apply -f deployment-billing-app-back-jenkins.yaml 2>&1
          '''
        }
      }
    }
  }
}

