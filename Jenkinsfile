pipeline {
    agent {
        node { 
            label 'docker' 
        }
    }
    stage('build'){
        docker build test .
    }
}