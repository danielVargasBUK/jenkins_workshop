pipeline {
    agent any
    stages {
        stage('TimeOutExampleSucess') {
            steps {
                script {
                    try {
                        timeout(time: 1, unit: 'MINUTES') {
                            echo "timeout step"
                            sleep 1
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
                        timeout(time: 60, unit: 'SECONDS') {
                            echo "timeout step"
                            sleep 1
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
        stage('GET commit SHA') {
            steps {
                script {
                    checkCommit()
                }
            }
        }
    }
}



void checkCommit() {
  // Obtener el último commit del repositorio donde está el Jenkinsfile
  String jenkinsRepoLastCommit = sh(
    script: "git rev-parse HEAD",
    returnStdout: true
  ).trim()
    println("El commit ${jenkinsRepoLastCommit} del Jenkinsfile se encuentra en la rama ${env.BRANCH_NAME}")
    println("El commit ${jenkinsRepoLastCommit[0..7]} del Jenkinsfile se encuentra en la rama ${env.BRANCH_NAME}")
}