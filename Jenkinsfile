pipeline {
    agent any
    tools {nodejs "NodeJS19"}
    stages {
     
    stage('Build') {
        steps {
            dir('code') {
                sh 'npm install'   
            }
        }
    }

    stage('Start the app') {
        steps {
            sh 'npm start'
        }
    }

  }
}