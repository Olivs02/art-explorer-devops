pipeline {
    agent any

    stages {
        stage('Cloner le dépôt') {
            steps {
                git branch: 'main', url: 'https://github.com/Olivs02/art-explorer-devops.git'
            }
        }

        stage('Installer Python') {
            steps {
                sh 'apt-get update && apt-get install -y python3 python3-pip'
            }
        }

        stage('Tests unitaires') {
            steps {
                sh 'python3 -m unittest discover tests'
            }
        }

        stage('Build Docker') {
            steps {
                sh 'docker build -t art-explorer .'
            }
        }
    }
}
