pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Build') {
      agent any
      steps {
        sh 'docker build -t dramos84/dp-alpine:latest .'
      }
    }
    stage('Login') {
      agent any
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      agent any
      steps {
        sh 'docker push dramos84/dp-alpine:latest'
      }
    }
  }
  post {
    always {
      agent any
      steps {
        sh 'docker logout'
      }
    }
  }
}
