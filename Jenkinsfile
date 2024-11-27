pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                // GitHub'dan kodları çek
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                // Gerekli Python bağımlılıklarını yükle
                sh 'pip install -r requirements.txt || echo "No requirements file"'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                // Uygulamayı çalıştırma
                sh 'python app.py'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Pytest'i yükle ve testleri çalıştır
                sh 'pip install pytest pytest-junitxml'
                sh 'pytest --junitxml=report.xml'
                junit 'report.xml' // Test raporlarını Jenkins'e ilet
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Deploy aşaması: burada deploy scripti veya işlemleri yer alır
                sh './deploy.sh || echo "No deployment script found"'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs() // Workspace temizliği
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Sending notification...'
            // Başarısızlık durumunda yapılacaklar
        }
    }
}
