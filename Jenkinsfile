pipeline {
    agent any
    stages {
        stage('TimeOutExampleSucess') {
            steps {
                script {
                    catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                        timeout(time: 1, unit: 'MINUTES') {
                            sh 'sleep 10' 
                        }
                    }
                }
            }
        }
        stage('TimeOutExampleFailure') {
            steps {
                script {
                    catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                        timeout(time: 1, unit: 'MINUTES') {
                            sh 'sleep 62' 
                        }
                    }
                }
            }
        }
    }
}