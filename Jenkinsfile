pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                script {
                    docker.image('ruby:3.3.5-alpine3.20').inside {
                        sh 'ruby --version'
                    }
                }
            }
        }
    }
}