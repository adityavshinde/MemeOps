pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/adityavshinde/MemeOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }
        stage('Build') {
            steps {
                sh 'python app.py'
            }
        }
    }
    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
