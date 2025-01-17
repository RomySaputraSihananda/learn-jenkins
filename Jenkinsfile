pipeline {
    agent {
        node { 
            label 'docker' 
        }
    }
    environment {
        CHAT_ID = '-4570371101'
    }
    stages {
        stage('Get Version Input') {
            steps {
                script {
                    def userInput = input(
                        id: 'userInput', message: 'Masukkan versi image:',
                        parameters: [
                            string(name: 'IMAGE_VERSION', defaultValue: '1.0.0', description: 'Masukkan versi image yang diinginkan')
                        ]
                    )
                    env.IMAGE_VERSION = userInput
                }
            }
        }
        stage('build') {
            steps {
                script {
                    sh 'docker build -t vite-app:${IMAGE_VERSION} .'
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                    sh 'docker run --rm -d -p 3000:3000 --name vite-app vite-app:${IMAGE_VERSION}'
                }
            }
        }
    }
    post {
        always {
            script {
                sh """
                curl -X POST https://api.telegram.org/bot${BOT_TOKEN}/sendMessage \
                -H "Content-Type: application/json" \
                -d '{"chat_id": "${CHAT_ID}", "text": "pipeline selesai", "disable_notification": true}'
                """
            }
        }
        success {
            script {
                sh """
                curl -X POST https://api.telegram.org/bot${BOT_TOKEN}/sendMessage \
                -H "Content-Type: application/json" \
                -d '{"chat_id": "${CHAT_ID}", "text": "Build and deployment succeeded for version ${IMAGE_VERSION}", "disable_notification": true}'
                """
            }
        }
        failure {
            script {
                sh """
                curl -X POST https://api.telegram.org/bot${env.BOT_TOKEN}/sendMessage \
                -H "Content-Type: application/json" \
                -d '{"chat_id": "${CHAT_ID}", "text": "Build or deployment failed for version ${IMAGE_VERSION}", "disable_notification": true}'
                """
            }
        }
    }
}
