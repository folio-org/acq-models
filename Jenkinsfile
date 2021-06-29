
pipeline {

  options {
    buildDiscarder(logRotator(numToKeepStr: '30', artifactNumToKeepStr: '30'))
  }

  agent {
    node {
      label 'jenkins-agent-java11'
    }
  }

  stages {
    stage('Prep') {
      steps {
        script {
          currentBuild.displayName = "#${env.BUILD_NUMBER}-${env.JOB_BASE_NAME}"
        }
        sendNotifications 'STARTED'
      }
    }

    stage('API schema lint') {
      steps {
        runApiSchemaLint('.', '')
      }
    }

  } // end stages

  post {
    always {
      sendNotifications currentBuild.result
    }
  }

}


