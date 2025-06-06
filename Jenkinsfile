pipeline {
    agent any

    environment {
        SLACK_CHANNEL = '#ci-cd'
        SLACK_CREDENTIAL_ID = 'slack-webhook'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
    }

    post {
        success {
            slackSend(
                channel: "${SLACK_CHANNEL}",
                color: 'good',
                message: "✅ Build SUCCESS for ${JOB_NAME} #${BUILD_NUMBER}",
                tokenCredentialId: "${SLACK_CREDENTIAL_ID}"
            )
        }
        failure {
            slackSend(
                channel: "${SLACK_CHANNEL}",
                color: 'danger',
                message: "❌ Build FAILED for ${JOB_NAME} #${BUILD_NUMBER}",
                tokenCredentialId: "${SLACK_CREDENTIAL_ID}"
            )
        }
    }
}
