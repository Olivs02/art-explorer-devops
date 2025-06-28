pipeline {
    agent any

    environment {
        PYTHONUNBUFFERED = 1
    }

    stages {
        stage('Setup Python Env') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run unit tests') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest tests/ || exit 1
                '''
            }
        }
    }

    post {
        failure {
            echo "Build échoué – tests unitaires"
        }
    }
}
