pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'python3 asd.py'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                // Test komutlarını buraya ekleyebilirsiniz
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Deploy işlemleri burada tanımlanabilir
            }
        }
    }
}
