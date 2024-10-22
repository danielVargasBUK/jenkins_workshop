pipeline {
    agent any
    stages {
        stage('TimeOutExampleSucess') {
            steps {
                script {
                    timeout(time: 1, unit: 'MINUTES', abort: true) {
                        sh 'sleep 30' 
                    }
                }
            }
        }
        stage('TimeOutExampleFailure') {
            steps {
                script {
                    timeout(time: 1, unit: 'MINUTES', abort: true) {
                        sh 'sleep 62' 
                    }
                }
            }
        }
    }
}