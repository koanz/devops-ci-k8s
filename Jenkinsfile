pipeline {
  agent any
  stages {
    stage('clone repository') {
      steps {
        powershell '''
          try {
            Write-Output "Checking Java version"
            java -version 2>&1
            Write-Output "Checking Maven version"
            mvn --version 2>&1
            Write-Output "Checking Git version"
            git --version 2>&1
          } catch {
            Write-Output "Error during version check: $_"
            throw $_
          }
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
              kubectl --token $env:api_token --server=http://localhost:8081 --insecure-skip-tls-verify=true apply -f deployment-billing-app-back-jenkins.yaml 2>&1
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

