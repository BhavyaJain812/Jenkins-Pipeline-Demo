pipeline {
    agent any

    environment {
        SLACK_WEBHOOK_URL = credentials('slack-webhook')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building project...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying project...'
            }
        }
    }

    post {
        success {
            slackSend(
                color: 'good',
                message: "✅ *Build Successful*: Job '${env.JOB_NAME} [#${env.BUILD_NUMBER}]' ran successfully.\nSee: ${env.BUILD_URL}",
                webhookUrl: SLACK_WEBHOOK_URL
            )
        }
        failure {
            slackSend(
                color: 'danger',
                message: "❌ *Build Failed*: Job '${env.JOB_NAME} [#${env.BUILD_NUMBER}]' failed.\nCheck logs: ${env.BUILD_URL}",
                webhookUrl: SLACK_WEBHOOK_URL
            )
        }
    }
}
