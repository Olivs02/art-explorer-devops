pipeline {
    agent any

    environment {
        PYTHONUNBUFFERED = 1
    }

    stages {
        stage('Install dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run unit tests') {
            steps {
                sh 'pytest tests/ || exit 1'
            }
        }
    }

    post {
        failure {
            echo "Build échoué – tests unitaires"
        }
    }
}
