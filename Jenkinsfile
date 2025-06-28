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
            script {
                sh '''
                    curl -H "Content-Type: application/json" \
                    -d '{"text": "Le build de *${JOB_NAME}* #${BUILD_NUMBER} a échoué. Voir : ${BUILD_URL}"}' \
                    https://reseauges75.webhook.office.com/webhookb2/a7ec4924-60f8-454b-8355-032da4999b0c@c371d4f5-b34f-4b06-9e66-517fed904220/IncomingWebhook/bfe38787b50f41d485857924c0e091ce/e49d4ff7-bcd8-48f9-8d04-ba8395809771/V2DkMfHfjx7yjGuWHDh2uW5XhZhj0lhlNMLV2LX7s5lHY1
                '''
            }
        }
    }
}
