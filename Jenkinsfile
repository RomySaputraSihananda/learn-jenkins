pipeline {
    agent {
        node { 
            label 'docker' 
        }
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
                    echo userInput
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
                    sh 'docker run --rm -d -p 3000:3000 -n vite-app vite-app:${IMAGE_VERSION}'
                }
            }
        }
    }
}
