pipeline {
  agent any
  environment {
    registry = "ybmsr/java-project"
    registryCredential = 'dockerhub_credentials'
    dockerImage = ''
  }
  stages {
    stage('Building image') {
      steps {
        script {
          dockerImage = docker.build("${registry}:${BUILD_NUMBER}")
        }
      }
    }
    stage('Push image') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', registryCredential) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove old docker image') {
      steps {
        sh "docker rmi ${registry}:${BUILD_NUMBER}"
      }
    }
  }
}


