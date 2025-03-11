pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
                echo 'Dependencies installed successfully'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
                echo 'Build Stage Successful'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
                echo 'Test Stage Successful'
            }
            post {
                always {
                    junit 'test-results.xml'  // Ensure your test framework generates this file
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'npm run deploy'
                echo 'Deployment Successful'
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed'
        }
    }
}
