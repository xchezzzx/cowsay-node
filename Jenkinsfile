//Oleg Milyukov

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

        stage("build & SonarQube analysis") {
            agent any
            steps {
                withSonarQubeEnv('SonarQube Server Test') {
                sh 'mvn clean package sonar:sonar'
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
                }
            }
        }

        // stage('Start the app') {
        //     steps {
        //         dir('code') {
        //             sh 'npm start'
        //         }
        //     }
        // }

    }
}