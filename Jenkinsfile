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
            $ErrorActionPreference = "Stop"
            kubectl --token $env:api_token --server=https://192.168.49.2:8443/ --insecure-skip-tls-verify=true apply -f deployment-billing-app-back-jenkins.yaml 2>&1
          '''
        }
      }
    }
  }
}

