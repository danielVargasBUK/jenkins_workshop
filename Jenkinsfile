pipeline {
    agent any
    stages {
        stage('TimeOutExampleSucess') {
            steps {
                script {
                    timeout(time: 1, unit: 'MINUTES') {
                        sh 'sleep 30' 
                    }
                }
            }
        }
        stage('TimeOutExampleFailure') {
            steps {
                script {
                    timeout(time: 1, unit: 'MINUTES') {
                        sh 'sleep 62' 
                    }
                }
            }
        }
    }
}