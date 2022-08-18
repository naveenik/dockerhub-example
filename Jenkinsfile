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
        echo "Build stage succcess"
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        echo "Login stage success"
      }
    }
    stage('Push') {
      steps {
        sh 'sudo docker push demo84/dp-alpine:latest'
        eccho "Push stage success"
      }
    }
  }
  post {
    always {
      sh 'sudo docker logout'
      echo "post stage success"
    }
  }
}
