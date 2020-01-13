pipeline {

  environment {
    registry = "fpacilio/apache"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/fpacilio/cicd-poc.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          withCredentials([usernamePassword( credentialsId: 'docker-hub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {    
          docker.withRegistry('', 'docker-hub-credentials') {
            sh "docker login -u ${USERNAME} -p ${PASSWORD}"
            dockerImage.push("${BUILD_NUMBER}")
            dockerImage.push("latest")
          }
        }
      }
    }
    }

    stage('Deploy App') {
      steps {
        script {
            sh 'export ID=`date +\"%s\"`; echo $ID; sed -i "s|PIPPO|$ID|" myweb.yaml'
            kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}