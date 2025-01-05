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
    }
}
