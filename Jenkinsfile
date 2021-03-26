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
                 slackSend baseUrl: 'https://hooks.slack.com/services/', 
                     channel: '#jenkinsintegration', 
                     color: 'Good', 
                     message: message: "*${currentBuild.currentResult}:* Job `${env.JOB_NAME}` build `${env.BUILD_DISPLAY_NAME}` by <@${env.GIT_AUTHOR}>\n Build commit: ${GIT_COMMIT}\n Last commit message: '${env.GIT_COMMIT_MSG}'\n More info at: ${env.BUILD_URL}\n Time: ${currentBuild.durationString.minus(' and counting')}",
                     teamDomain: 'Jenkins_Testing', 
                     tokenCredentialId: 'SlackId', 
                     username: 'rajshan17'
            }
        }
        }
     }
