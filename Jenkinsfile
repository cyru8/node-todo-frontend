pipeline {
  // environment {
  //   registry = "oadetiba/node-todo-frontend"
  //   registryCRedential = "dockerhub"
  // }
  // agent any
  agent {
    docker {
        image 'node:lts-buster-slim'
        // args '-p 3000:3000'
    }
  }
  // agent {
  //   label 'node2'
  // }
  stages {
    stage("Cloning Git repo for node-todo-frontend") {
      steps {
        git "https://github.com/cyru8/node-todo-frontend.git"
      }
    }
    // stage ("Build Docker Image for nodejs frontend application") {
    //   steps{
    //     script {
    //       docker.build registry + ":$BUILD_NUMBER"
    //     }
    //   }
    // }
    stage("Build image with the node-todo-frontend App and Push the Image to Docker Registry") {
      steps {
        echo "Workspace is $WORKSPACE"
        dir("$WORKSPACE") {
            script {
                docker.withRegistry('', 'DockerHub') {
                            def image = docker.build('oadetiba/node-todo-frontend:v$BUILD_NUMBER')
                            echo "Please proceed to push the images: node-todo-frontend"
                            image.push()
                slackSend message: "node-todo-frontend image built and pushed - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL} | Link>)"
            }
          }
        }
      }                
    }      
  }
}