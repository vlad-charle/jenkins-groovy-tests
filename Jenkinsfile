def gv

pipeline {

  agent any

  stages {
    stage('Load Groovy script') {
      steps{
        script {
          gv = load "script.groovy"
        }
      }
    }
    stage('Build image') {
      steps{
        script {
          gv.buildImage()
        }
      }
    }
    stage('Push Image') {
      steps{
        script {
          gv.pushImage()
        }
      }
    }
  }
  post {
    success {
        slackSend color: 'good', message: 'Build succesful: ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)'
    }
    failure {
        slackSend color: 'danger', message: 'Build failed: ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)'
    }
  }
}