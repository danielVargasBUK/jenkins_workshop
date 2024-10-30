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

    println("El commit del env ${env.GIT_COMMIT}")
    println("El commit del env ${env.GIT_COMMIT[0..7]}")

    if (jenkinsRepoLastCommit != env.GIT_COMMIT) {
        error "El commit del Jenkinsfile no coincide con el commit del repositorio"
    }else{
        println "El commit del Jenkinsfile coincide con el commit del repositorio"
    }
}