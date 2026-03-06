pipeline {
    agent any

    environment {
        IMAGE_NAME = "python-web-server"
        CONTAINER_NAME = "python-web-container"
    }

    stages {

        stage('Checkout') {
            steps {
                echo "Cloning repository"
                git branch: 'main', url: 'https://github.com/veerbasanna/docker-feature-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image"
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Container') {
            steps {
                echo "Running Docker container"
                sh '''
                docker rm -f $CONTAINER_NAME || true
                docker run -d -p 8000:8000 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }

        stage('Test Application') {
            steps {
                echo "Testing application"
                sh 'curl http://localhost:8000'
            }
        }

    }
}
