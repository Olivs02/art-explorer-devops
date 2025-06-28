pipeline {
    agent {
        docker {
            image 'python:3.10-slim'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
        stage('Tests unitaires') {
            steps {
                sh 'pip install -r requirements.txt'
                sh 'python -m unittest discover tests'
            }
        }

        stage('Build Docker') {
            steps {
                sh 'docker build -t art-explorer .'
            }
        }
    }
}
