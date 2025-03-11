pipeline {
    agent any

    environment {
        APP_NAME = "myapp"
        DOCKER_IMAGE = "myapp:latest"
        DEPLOY_SERVER = "user@server:/path/to/deploy"
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Starting Build Stage...'
                    sh 'npm install'
                    echo 'Build Stage Successful'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Starting Test Stage...'
                    sh 'npm test'
                    echo 'Test Stage Successful'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Starting Deployment...'
                    sh 'docker build -t $DOCKER_IMAGE .'
                    sh 'docker run -d -p 80:80 $DOCKER_IMAGE'
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
            sh 'docker system prune -f'
        }
    }
}
