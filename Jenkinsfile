pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                // سحب الكود من مستودعك
                git branch: 'main', url: 'https://github.com/Ehabayman21/jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building the image..."
                // بناء الصورة باسم php-app
                sh 'docker build -t php-app .'
            }
        }

        stage('Run Container') {
            steps {
                echo "Running the container on port 8070..."
                // حذف الحاوية القديمة إذا كانت موجودة لتجنب الخطأ
                sh 'docker stop php-app || true'
                sh 'docker rm php-app || true'
                // تشغيل الحاوية الجديدة على بورت 8070
                sh 'docker run -d -p 8070:80 --name php-app php-app'
            }
        }
    }

    post {
        success {
            echo "Congratulations! Access your app at http://localhost:8070"
        }
        failure {
            echo "Pipeline failed. Check the console output for errors."
        }
    }
}