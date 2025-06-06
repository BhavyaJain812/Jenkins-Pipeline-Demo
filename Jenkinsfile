pipeline {
    agent any

    environment {
        // Load the webhook URL from Jenkins credentials
        SLACK_WEBHOOK_URL = credentials('slack-webhook')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Running build step...'
                // Simulate a build step
                sh 'exit 0' // Change to 'exit 1' to simulate failure
            }
        }
    }

    post {
        success {
            script {
                slackNotify("✅ Build Succeeded in Job: ${env.JOB_NAME} #${env.BUILD_NUMBER}")
            }
        }
        failure {
            script {
                slackNotify("❌ Build Failed in Job: ${env.JOB_NAME} #${env.BUILD_NUMBER}")
            }
        }
    }
}

def slackNotify(String message) {
    // Send message to Slack using webhook
    sh """
        curl -X POST -H 'Content-type: application/json' \
        --data '{"text": "${message}"}' \
        ${SLACK_WEBHOOK_URL}
    """
}
