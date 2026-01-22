pipeline {
    agent any

    stages {
        stage('Build Image') {
            steps {
                sh 'docker build -t php-app .'
            }
        }

        stage('Test') {
            steps {
                echo "Testing if the container starts correctly..."
                sh 'docker run -d --name test-container -p 8085:80 php-app'
                // ننتظر ثواني للتأكد أن Apache بدأ العمل
                sleep 5
                // نختبر إذا كان السيرفر يرد بـ HTTP 200 (ناجح)
                sh 'curl -s --head  http://localhost:8085 | grep "200 OK"' 
                echo "Test Passed! ✅"
                // نحذف حاوية الاختبار
                sh 'docker rm -f test-container'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker rm -f php-app || true'
                sh 'docker run -d -p 8070:80 --name php-app php-app'
            }
        }
    }
}