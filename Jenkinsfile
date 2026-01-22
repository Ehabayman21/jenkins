pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                echo "Cloning project from GitHub..."
                git 'https://github.com/Ehabayman21/jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh 'docker build -t php-app .'
            }
        }

        stage('Run Container') {
            steps {
                echo "Running Docker container..."
                sh '''
                    docker stop php-app || true
                    docker rm php-app || true
                    docker run -d -p 8070:80 --name php-app php-app
                '''
            }
        }
    }

    post {
        success {
            echo "App is running successfully 🚀"
        }
        failure {
            echo "Something went wrong ❌"
        }
    }
}