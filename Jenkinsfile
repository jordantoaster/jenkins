pipeline {

  environment {
    registry = $params.docker-hub-repository // target Jenkins Repository - parameter input on build
    registryCredential = 'dockerhub' // registered in Jenknis credentials
    dockerImage = ''
  }

  // default agent
  agent any

  stages {

    stage('Cloning Git') {
      steps {
        git 'https://github.com/jordantoaster/jenkins.git'
      }
    }

    stage('test') {

        agent { // use project docker file to run the tests
            dockerfile {
                filename 'Dockerfile'
            }
        }  

        steps {
            sh 'python -m pytest'
        }   
    }

    stage('Building image') { // use the docker file to build.
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