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
            withCredentials([string(credentialsId: 'slack-webhook', variable: 'SLACK_WEBHOOK_URL')]) {
                slackSend(
                    webhookUrl: "${env.SLACK_WEBHOOK_URL}",
                    message: "Build Successful: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
                )
            }
        }
        failure {
            withCredentials([string(credentialsId: 'slack-webhook', variable: 'SLACK_WEBHOOK_URL')]) {
                slackSend(
                    webhookUrl: "${env.SLACK_WEBHOOK_URL}",
                    message: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
                )
            }
        }
    }
}
