pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-app"
        IMAGE_TAG = "latest"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                    docker rm -f my-app-container || true
                    docker run -d \
                      --name my-app-container \
                      -p 8080:5000 \
                      ${IMAGE_NAME}:${IMAGE_TAG}
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }

        success {
            echo 'Build succeeded.'
        }

        failure {
            echo 'Build failed.'
        }
    }
}
