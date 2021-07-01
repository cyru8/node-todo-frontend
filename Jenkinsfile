pipeline {
  // environment {
  //   registry = "oadetiba/node-todo-frontend"
  //   registryCRedential = "dockerhub"
  // }
  // agent any
  // agent {
  //   docker {
  //       image 'node:lts-buster-slim'
  //       args '-p 3000:3000'
  //   }
  // }
  agent {
    label 'docker'
  }
  stages {
    stage("Cloning Git repo for node-todo-frontend") {
      steps {
        git "https://github.com/cyru8/node-todo-frontend.git"
      }
    }
    stage ("Build Docker Image for nodejs frontend application") {
      steps{
        script {
          docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }      
  }
}