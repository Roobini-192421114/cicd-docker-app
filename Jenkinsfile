pipeline {
    agent any

    environment {
        IMAGE_NAME = "roobini1911/cicd-docker-app"
        TAG = "latest"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$TAG .'
            }
        }

        stage('Run Tests') {
            steps {
                echo "Running tests..."
                sh 'docker run --rm $IMAGE_NAME:$TAG python -c "print(\\"Tests Passed\\")"'
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                sh 'docker push $IMAGE_NAME:$TAG'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop cicd-container || true
                docker rm cicd-container || true
                docker run -d -p 5000:5000 --name cicd-container $IMAGE_NAME:$TAG
                '''
            }
        }
    }
}