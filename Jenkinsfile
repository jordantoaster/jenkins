pipeline {

  environment {
    registry = "jordantoaster/jenkins-example"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }

//   agent {
//     dockerfile {
//       filename 'Dockerfile'
//     }
//   }  

  agent any

  stages {

    stage('Cloning Git') {
      steps {
        git 'https://github.com/jordantoaster/jenkins.git'
      }
    }

    stage('test') {
      steps {
        sh 'python -m pytest'
      }   
    }

    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
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