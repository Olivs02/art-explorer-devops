pipeline {
    agent any

    stages {
        stage('Cloner le dépôt') {
            steps {
                git branch: 'main', url: 'https://github.com/Olivs02/art-explorer-devops.git'
            }
        }

        stage('Tests unitaires') {
            steps {
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
