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
}