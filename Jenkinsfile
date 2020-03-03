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
          sh "pwd"
          sh "whoami"
          sh "sudo kubectl apply -f /var/lib/jenkins/workspace/deploy_application/deployment.yml"
          //sh "kubectl apply -f https://k8s.io/examples/application/deployment-scale.yaml"
          //sh "kubectl expose deployment tomcat-deployment --type=NodePort --name=tomcat-service"
          //sh "minikube service tomcat-service --url"
        }
      }
    }
  }
}
