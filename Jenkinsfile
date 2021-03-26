pipeline {
    agent any
     stages {
        stage('SCM Checkout') {
            agent any
            steps {
                git 'https://github.com/rajshan17/mvn_sonar'
            }
        }
        stage('Build') {
            agent{
                docker {
                    image 'maven:3-alpine' 
                    args '-v /root/.m2:/root/.m2' 
                }
            }
            steps {
                 sh 'mvn -B -DskipTests clean package sonar:sonar'               
                 slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#jenkinsintegration', color: 'Good', message: 'Build Success', teamDomain: 'Jenkins_Testing', tokenCredentialId: 'SlackId', username: 'rajshan17'
            }
        }
        }
     }
