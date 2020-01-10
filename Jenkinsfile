pipeline {
  agent any
  stages {
    stage('Checkout Source') {
      steps {
        git 'https://github.com/fpacilio/cicd-poc.git'
      }
    }
    stage('Build image') {
      steps {
        sh '''        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }'''
        }
      }
    }
    environment {
      registry = 'fpacilio/apache'
      dockerImage = ''
    }
  }