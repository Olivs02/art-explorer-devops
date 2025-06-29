pipeline {
    agent any

    environment {
        PYTHONUNBUFFERED = 1
    }

    stages {
        stage('Install Python & pip') {
            steps {
                sh '''
                    apt-get update
                    apt-get install -y python3 python3-pip python3-venv
                '''
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'python3 -m venv venv && . venv/bin/activate && pip install -r requirements.txt'
            }
        }

        stage('Run unit tests') {
            steps {
                sh '. venv/bin/activate && pytest tests/ || exit 1'
            }
        }

        stage('Deploy to VM') {
            steps {
                sshagent(['vm-ssh-key']) {
                    sh 'scp -o StrictHostKeyChecking=no -r * jenkins@192.168.100.170:/home/jenkins/app'
                }
            }
        }
    }

    post {
        failure {
            script {
                sh """
                    curl -H "Content-Type: application/json" \
                    -d '{"text": " Le build de *${env.JOB_NAME}* #${env.BUILD_NUMBER} a échoué. Voir : ${env.BUILD_URL}"}' \
                    https://reseauges75.webhook.office.com/webhookb2/a7ec4924-60f8-454b-8355-032da4999b0c@c371d4f5-b34f-4b06-9e66-517fed904220/IncomingWebhook/bfe38787b50f41d485857924c0e091ce/e49d4ff7-bcd8-48f9-8d04-ba8395809771/V2DkMfHfjx7yjGuWHDh2uW5XhZhj0lhlNMLV2LX7s5lHY1
                """
            }
        }
    }
}
