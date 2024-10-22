pipeline {
    try agent { any { image  { image 'ruby:3.3.5-alpine3.20' } }
    stages {
        stage('build') {
            steps {
                sh 'ruby --version'
            }
        }
    }
}