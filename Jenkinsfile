pipeline {
    agent any
    stages {
        stage('Test Slack') {
            steps {
                withCredentials([string(credentialsId: 'slack-webhook', variable: 'SLACK_WEBHOOK_URL')]) {
                    slackSend webhookUrl: "${env.SLACK_WEBHOOK_URL}", message: "Hello from Jenkins!"
                }
            }
        }
    }
}
