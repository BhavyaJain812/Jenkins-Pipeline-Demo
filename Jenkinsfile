pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
    }

    post {
        success {
            slackSend channel: '#all-jenkinsdemo', 
                      tokenCredentialId: 'slack-webhook', 
                      message: "Build Successful: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
        }
        failure {
            slackSend channel: '#all-jenkinsdemo', 
                      tokenCredentialId: 'slack-webhook', 
                      message: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
        }
    }
}
