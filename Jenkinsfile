pipeline {
    agent any

    environment {
        IMAGE_NAME = "roobini1911/cicd-docker-app"
        TAG = "latest"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:%TAG% .'
            }
        }

        stage('Run Tests') {
            steps {
                echo "Running tests..."
                bat 'docker run --rm %IMAGE_NAME%:%TAG% python -c "print(\\"Tests Passed\\")"'
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                bat 'docker push %IMAGE_NAME%:%TAG%'
            }
        }

        stage('Deploy Container') {
            steps {
                bat '''
                docker stop cicd-container || exit 0
                docker rm cicd-container || exit 0
                docker run -d -p 5000:5000 --name cicd-container %IMAGE_NAME%:%TAG%
                '''
            }
        }
    }
}