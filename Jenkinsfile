//Oleg Milyukov

pipeline {
    agent any
    tools {
        nodejs "NodeJS19"
        maven 'Maven 3.9.1'
        }
    stages {
     
        stage('Install dependencies') {
            steps {
                dir('code') {
                    sh 'npm install'   
                }
            }
        }


        stage('Get Git Branch') {
            steps {
                script {
                    def branchName = env.GIT_BRANCH
                    echo "Git Branch: ${branchName}"
                }
            }
        }

        // stage('SonarQube analysis') {
        //     agent any
        //     steps {
        //         dir('code') {
        //             withSonarQubeEnv('sonarqube-10.0') {
        //             sh "mvn clean package sonar:sonar"
        //             }
        //         }
        //     }
        // }

        stage('SonarQube analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarQubeScanner-4.8.0';
                    withSonarQubeEnv('sonarqube-10.0') { 
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=cowsay-ex"
                    }
                }
            }
        }

        // stage('Quality Gate') {
        //     steps {
        //         timeout(time: 1, unit: 'HOURS') {
        //         waitForQualityGate abortPipeline: true
        //         }
        //     }
        // }

        stage('Sending notification') {
            steps {
                slackSend(
                    channel: '#general',
                    color: 'good',
                    message: "Step ${currentBuild.fullDisplayName} succeeded!",
                    token: 'slack-token'
                )
            }
        }

        stage('Start the app') {
            steps {
                dir('code') {
                    sh 'npm start'
                    sh 'sleep 60'
                    sh 'fuser -k 8081/tcp'
                }
            }
        }
    }
}