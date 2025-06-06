pipeline {
    agent any

    environment {
        // Replace this with your actual Slack credential ID from Jenkins
        SLACK_CREDENTIAL_ID = 'slack-webhook'
        // Use your Slack channel name (case-sensitive), must start with '#'
        SLACK_CHANNEL = '#all-jenkinsdemo'
    }

    stages {
        stage('Clone') {
            steps {
                echo '📥 Cloning repository...'
                // Git step not needed here since Jenkins already pulls from SCM
            }
        }

        stage('Build') {
            steps {
                echo '🔨 Building the project...'
                // Add build commands here, e.g., sh './build.sh'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                // Add test commands here, e.g., sh './run-tests.sh'
            }
        }
    }

    post {
        success {
            slackSend(
                channel: "${env.SLACK_CHANNEL}",
                color: 'good',
                message: "✅ SUCCESS: *${env.JOB_NAME}* #${env.BUILD_NUMBER} \n🔗 <${env.BUILD_URL}|View Build>",
                tokenCredentialId: "${env.SLACK_CREDENTIAL_ID}"
            )
        }

        failure {
            slackSend(
                channel: "${env.SLACK_CHANNEL}",
                color: 'danger',
                message: "❌ FAILURE: *${env.JOB_NAME}* #${env.BUILD_NUMBER} \n🔗 <${env.BUILD_URL}|View Build>",
                tokenCredentialId: "${env.SLACK_CREDENTIAL_ID}"
            )
        }

        always {
            slackSend(
                channel: "${env.SLACK_CHANNEL}",
                color: '#439FE0',
                message: "ℹ️ FINISHED: *${env.JOB_NAME}* #${env.BUILD_NUMBER} \n🔗 <${env.BUILD_URL}|View Build>",
                tokenCredentialId: "${env.SLACK_CREDENTIAL_ID}"
            )
        }
    }
}
