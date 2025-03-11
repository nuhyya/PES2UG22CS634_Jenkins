pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/nuhyya/PES2UG22CS634_Jenkins.git'
            }
        }

        stage('Build') {
            steps {
                sh 'g++ -o PES2UG22CS634-1 hi.cpp'
                echo 'Build Stage Successful'
            }
        }

        stage('Test') {
            steps {
                sh './PES2UG22CS634-1'
                echo 'Test Stage Successful'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh '''
                chmod +x PES2UG22CS634-1
                mv PES2UG22CS634-1 $HOME/bin/ || echo "Move failed, check permissions!"
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
