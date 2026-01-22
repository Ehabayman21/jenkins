pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                // بناء الصورة
                sh 'docker build -t php-app .'
            }
        }

        stage('Run Container') {
            steps {
                echo "Deploying container on port 8070..."
                // حذف الحاوية القديمة قسرياً إذا كانت موجودة لتجنب تعارض الأسماء
                sh 'docker rm -f php-app || true'
                // تشغيل الحاوية الجديدة على بورت 8070
                sh 'docker run -d -p 8070:80 --name php-app php-app'
            }
        }
    }

    post {
        success {
            echo "Success! Access your app at http://localhost:8070"
        }
        failure {
            echo "Something went wrong ❌"
        }
    }
}