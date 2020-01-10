pipeline {
  agent any
  stages {
    stage('Checkout Source') {
      steps {
        git 'https://github.com/fpacilio/cicd-poc.git'
      }
    }
  }
  environment {
    registry = 'fpacilio/apache'
    dockerImage = ''
  }
}