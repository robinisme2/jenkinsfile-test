pipeline {
    agent {
        docker { image 'node:16.13.1-alpine' }
    }
    stages {
        stage('Test') {
            steps {
                sh '/usr/local/bin/node --version'
            }
        }
    }
}
