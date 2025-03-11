pipeline {
    agent any

    environment {
        APP_NAME = "mycppapp"
        DEPLOY_SERVER = "user@server:/path/to/deploy"
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Starting Build Stage...'
                    sh 'make'
                    echo 'Build Stage Successful'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Starting Test Stage...'
                    sh './run_tests.sh'
                    echo 'Test Stage Successful'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Starting Deployment...'
                    sh 'scp mycppapp $DEPLOY_SERVER'
                    echo 'Deployment Successful'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully! 🎉'
        }

        failure {
            echo 'Pipeline failed ❌'
            slackSend channel: '#devops', message: "Jenkins Pipeline Failed!", color: 'danger'
        }

        always {
            echo 'Cleaning up workspace...'
        }
    }
}
