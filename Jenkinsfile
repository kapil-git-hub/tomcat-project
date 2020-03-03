pipeline {
  environment {
    registry = "kapil14/myrepo"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/kapil-git-hub/tomcat-project.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage ('Deploy App') {
      steps {
        script{
          sh "kubectl apply -f deployment.yaml"
        }
      }
    }
  }
}
