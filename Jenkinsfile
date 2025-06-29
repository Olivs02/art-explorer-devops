pipeline {
    agent {
        docker {
            image 'python:3.10-slim'
        }
    }

    environment {
        PYTHONUNBUFFERED = 1
    }

    stages {
        stage('Install dependencies') {
            steps {
                sh '''
                    apt-get update && apt-get install -y python3-venv python3-pip
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run unit tests') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest tests/
                '''
            }
        }
    }
}
