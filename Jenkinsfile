pipeline {

  environment {
    registry = "jordantoaster/jenkins-example"
    registryCredential = 'dockerhub'
  }

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
    
    stage('Building image') {
      steps{
        script {
          docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
  }
}