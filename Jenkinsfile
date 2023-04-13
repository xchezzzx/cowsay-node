pipeline {
    agent any
    tools {nodejs "NodeJS19"}
    stages {
     
    stage('Build') {
        steps {
            sh 'rm ./package-lock.json && npm i'
        }
    }

    stage('Start the app') {
        steps {
            sh 'npm start'
        }
    }

  }
}