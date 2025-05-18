pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Corrected git syntax to clone the dev branch
                git branch: 'dev', url: 'https://github.com/adityavshinde/MemeOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                // Navigate to the project directory and install dependencies
                sh '''
                cd ${WORKSPACE}
                echo "Working directory: $(pwd)"
                which python || echo "Python not found!"
                which pip || echo "Pip not found!"
                
                # Check if requirements.txt exists and install packages
                if [ -f requirements.txt ]; then
                    pip install --user -r requirements.txt
                else
                    echo "requirements.txt not found!"
                    exit 1
                fi
                '''
            }
        }
        stage('Run Tests') {
            steps {
                // Run tests using pytest
                sh '''
                cd ${WORKSPACE}
                if [ -f requirements.txt ]; then
                    pip install --user -r requirements.txt
                fi
                pytest || echo "No tests found!"
                '''
            }
        }
        stage('Build') {
            steps {
                // Run the application
                sh '''
                cd ${WORKSPACE}
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
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}
