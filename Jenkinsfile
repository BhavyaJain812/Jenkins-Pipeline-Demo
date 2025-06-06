pipeline {
    agent any

    environment {
        SLACK_WEBHOOK = credentials('slack-webhook')
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
            sh """
                curl -X POST -H 'Content-type: application/json' \\
                --data '{"text":"✅ *Build Succeeded* for Job: ${env.JOB_NAME} #${env.BUILD_NUMBER}\\n${env.BUILD_URL}"}' \\
                ${SLACK_WEBHOOK}
            """
        }
        failure {
            sh """
                curl -X POST -H 'Content-type: application/json' \\
                --data '{"text":"❌ *Build Failed* for Job: ${env.JOB_NAME} #${env.BUILD_NUMBER}\\n${env.BUILD_URL}"}' \\
                ${SLACK_WEBHOOK}
            """
        }
    }
}
