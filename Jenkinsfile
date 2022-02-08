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
    stage('Sonar code check') {
      steps {
        script {
          def scannerHome = tool 'SonarScanner';
          withSonarQubeEnv('SQ') {
            sh "${scannerHome}/bin/sonar-scanner"
          }
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
        slackSend color: 'good', message: "Build succesful: ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
    }
    failure {
        slackSend color: 'danger', message: "Build failed: ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
    }
  }
}