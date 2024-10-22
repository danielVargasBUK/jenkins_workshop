pipeline {
    agent any
    stages {
        stage('TimeOutExampleSucess') {
            steps {
                script {
                    try {
                        timeout(time: 1, unit: 'MINUTES') {
                            echo "timeout step"
                            sleep 5
                        }
                    } catch(err) {
                        // timeout reached
                        println err
                        echo 'Time out reached.'
                        error 'build timeout failed'
                    }
                }
            }
        }
        stage('TimeOutExampleFailure') {
            steps {
                script {
                    try {
                        timeout(time: 1, unit: 'SECONDS') {
                            echo "timeout step"
                            sleep 5
                        }
                    } catch(err) {
                        // timeout reached
                        println err
                        echo 'Time out reached.'
                        error 'build timeout failed'
                    }
                }
            }
        }
    }
}