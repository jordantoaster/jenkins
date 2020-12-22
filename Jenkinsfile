pipeline {

  environment {
    registry = "jordantoaster/jenkins-example"
    registryCredential = 'dockerhub'
    dockerImage = ''
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

    stage('Deploy Image') {
        steps{
            script {
                docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()
                }
            }
        }
    }

    stage('Remove Unused docker image') {
        steps{
            sh "docker rmi $registry:$BUILD_NUMBER"
        }
    }
  }
}