pipeline {
  agent any
   
  stages {
     
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Start the app') {
        steps {
            sh 'npm start'
        }
    }

  }
}