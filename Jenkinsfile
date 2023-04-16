//Oleg Milyukov

pipeline {
    agent any
    tools {nodejs "NodeJS19"}
    stages {
     
        stage('Install dependencies') {
            steps {
                dir('code') {
                    sh 'npm install'   
                }
                try {
                    slackSend(
                    channel: '#general',
                    color: 'good',
                    message: "Step ${currentBuild.fullDisplayName} succeeded!",
                    tokenCredentialId: 'slack-token'
                )
                } catch (Exception e) {
                    echo "Error while sending Slack notification: ${e.message}"
                }
            }
        }

        stage('SonarQube analysis') {
            agent any
            steps {
                withSonarQubeEnv('SonarQube Server Test') {
                sh 'mvn clean package sonar:sonar'
                }
            }
        }
        stage('Quality Gate') {
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