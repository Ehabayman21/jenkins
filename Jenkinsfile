pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                // سحب الكود من فرع main كما هو ظاهر في صورك
                git branch: 'main', url: 'https://github.com/Ehabayman21/jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // بناء الصورة بناءً على الـ Dockerfile
                sh 'docker build -t php-app .'
            }
        }

        stage('Run & Deploy') {
            steps {
                // تنظيف أي حاوية قديمة بنفس الاسم لتجنب تكرار الاسم
                sh 'docker stop php-app || true'
                sh 'docker rm php-app || true'
                // التشغيل على بورت 8070 لتجنب بورت جينكينز 8080
                sh 'docker run -d -p 8070:80 --name php-app php-app'
            }
        }
    }

    post {
        success {
            echo "Congratulations! Application is running at http://localhost:8070"
        }
    }
}