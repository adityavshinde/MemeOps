pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Corrected the git syntax
                git branch: 'dev', url: 'https://github.com/adityavshinde/MemeOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                // Ensure that Python and pip are available
                sh '''
                which python || echo "Python not found!"
                which pip || echo "Pip not found!"
                pip install -r requirements.txt
                '''
            }
        }
        stage('Run Tests') {
            steps {
                // Run tests using pytest
                sh '''
                if [ -f requirements.txt ]; then
                    pip install -r requirements.txt
                fi
                pytest
                '''
            }
        }
        stage('Build') {
            steps {
                // Run the application
                sh '''
                if [ -f app.py ]; then
                    python app.py
                else
                    echo "app.py not found!"
                    exit 1
                fi
                '''
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
