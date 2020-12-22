pipeline {
  agent {
    dockerfile {
      filename 'Dockerfile'
    }
  }  
  stages {
    stage('test') {
      steps {
        sh 'python -m pytest'
      }   
    }
  }
}