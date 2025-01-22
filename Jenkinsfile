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
            try {
              $ErrorActionPreference = "Stop"
              kubectl --token $env:api_token --server=http://192.168.49.2:8443 --insecure-skip-tls-verify=true apply -f deployment-billing-app-back-jenkins.yaml
            } catch {
              Write-Output "Error during kubectl apply: $_"
              throw $_
            }
          '''
        }
      }
    }
  }
}

