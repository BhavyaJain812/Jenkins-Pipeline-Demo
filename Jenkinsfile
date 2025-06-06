pipeline {
    agent any

    stages {
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
        success {
            withCredentials([string(credentialsId: 'slack-webhook', variable: 'WEBHOOK_URL')]) {
                script {
                    def payload = '{"text": "✅ Build *SUCCESSFUL* for job: ' + env.JOB_NAME + ' #'+ env.BUILD_NUMBER + '"}'
                    httpRequest httpMode: 'POST',
                                url: "${WEBHOOK_URL}",
                                requestBody: payload,
                                contentType: 'APPLICATION_JSON'
                }
            }
        }

        failure {
            withCredentials([string(credentialsId: 'slack-webhook', variable: 'WEBHOOK_URL')]) {
                script {
                    def payload = '{"text": "❌ Build *FAILED* for job: ' + env.JOB_NAME + ' #'+ env.BUILD_NUMBER + '"}'
                    httpRequest httpMode: 'POST',
                                url: "${WEBHOOK_URL}",
                                requestBody: payload,
                                contentType: 'APPLICATION_JSON'
                }
            }
        }
    }
}
