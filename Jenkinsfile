pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('docker')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t pipelinejenkins/cicd-jenkins:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push  pipelinejenkins/cicd-jenkins:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
