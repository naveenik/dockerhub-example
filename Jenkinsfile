pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('demo84-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'sudo docker build -t demo84/dp-alpine:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'sudo docker push demo84/dp-alpine:latest'
      }
    }
  }
  post {
    always {
      sh 'sudo docker logout'
    }
  }
}
