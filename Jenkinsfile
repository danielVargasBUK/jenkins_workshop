pipeline {
    agent any
    stages {
        stage('TimeOutExampleSucess') {
            steps {
                script {
                    try {
                        timeout(time: 1, unit: 'MINUTES') {
                            sh 'sleep 10'
                        }
                    } catch (err) {
                        echo "Stage failed due to timeout: ${err}"
                        currentBuild.result = 'FAILURE'
                        error("Stage failed due to timeout.")
                    }
                }
            }
        }
        stage('TimeOutExampleFailure') {
            steps {
                script {
                    try {
                        timeout(time: 1, unit: 'MINUTES') {
                            sh 'sleep 62'
                        }
                    } catch (err) {
                        echo "Stage failed due to timeout: ${err}"
                        currentBuild.result = 'FAILURE'
                        error("Stage failed due to timeout.")
                    }
                }
            }
        }
    }
}