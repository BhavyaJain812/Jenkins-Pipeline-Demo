pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo '📥 Cloning repository...'
            }
        }
        stage('Build') {
            steps {
                echo '🔨 Building the project...'
            }
        }
        stage('Test') {
            steps {
                echo '🧪 Running tests...'
            }
        }
    }

    post {
        always {
            slackSend (
                channel: '#all-jenkinsdemo',
                color: '#439FE0',
                message: "ℹ️ FINISHED: *${env.JOB_NAME}* #${env.BUILD_NUMBER} \n🔗 <${env.BUILD_URL}|View Build>"
            )
        }
        success {
            slackSend (
                channel: '#all-jenkinsdemo',
                color: 'good',
                message: "✅ SUCCESS: *${env.JOB_NAME}* #${env.BUILD_NUMBER} \n🔗 <${env.BUILD_URL}|View Build>"
            )
        }
        failure {
            slackSend (
                channel: '#all-jenkinsdemo',
                color: 'danger',
                message: "❌ FAILURE: *${env.JOB_NAME}* #${env.BUILD_NUMBER} \n🔗 <${env.BUILD_URL}|View Build>"
            )
        }
    }
}
