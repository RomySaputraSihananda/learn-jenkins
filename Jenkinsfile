pipeline {
    agent {
        node { 
            label 'docker' 
        }
    }
    stages {
        stage('build') {
            steps {
                script {
                    sh 'docker build -t test .'
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                    sh 'docker run --rm -d -p 3000:3000 test'
                }
            }
        }
    }
}
