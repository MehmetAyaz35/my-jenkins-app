pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Creating virtual environment and installing dependencies...'
                // Virtual environment oluştur ve bağımlılıkları yükle
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install -r requirements.txt || echo "No requirements file"
                '''
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                // Virtual environment kullanarak uygulamayı çalıştır
                sh '''
                . venv/bin/activate
                python3 app.py
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Test bağımlılıklarını yükle ve testleri çalıştır
                sh '''
                . venv/bin/activate
                pip install pytest pytest-junitxml
                pytest --junitxml=report.xml
                '''
                junit 'report.xml' // Test raporlarını Jenkins'e ilet
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Deploy aşaması
                sh './deploy.sh || echo "No deployment script found"'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Sending notification...'
        }
    }
}
