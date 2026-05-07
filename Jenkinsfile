pipeline {
    agent any

    stages {

        stage('Build Stage') {
            steps {
                echo 'Building application...'
            }
        }

        stage('Test Stage') {
            steps {
                echo 'Running tests...'
                sh 'python3 --version || true'
            }
        }

        stage('Deploy Stage') {
            steps {
                echo 'Deploying application...'
            }
        }
    }
}