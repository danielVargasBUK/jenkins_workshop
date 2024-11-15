pipeline {
    agent any
    stages {
        stage('TimeOutExampleSuccess') {
            steps {
                script {
                    withTimeout(1, 'MINUTES', {
                        echo "timeout step"
                        sleep 1
                    }, 'Time out reached for TimeOutExampleSuccess.')
                }
            }
        }
        stage('TimeOutExampleFailure') {
            steps {
                script {
                    withTimeout(60, 'SECONDS', {
                        echo "timeout step"
                        sleep 1 // Esto fallará para probar el timeout
                    }, 'Time out reached for TimeOutExampleFailure.')
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

// Función genérica para manejar el timeout
void withTimeout(int time, String unit, Closure action, String errorMessage) {
    try {
        timeout(time: time, unit: unit) {
            action.call()
        }
    } catch (err) {
        println err
        echo errorMessage
        error errorMessage
    }
}

void checkCommit() {
    sh "git fetch origin ${env.BRANCH_NAME}"
    String jenkinsRepoLastCommit = sh(
        script: "git rev-parse origin/${env.BRANCH_NAME}",
        returnStdout: true
    ).trim()
    println("El commit ${jenkinsRepoLastCommit} del Jenkinsfile se encuentra en la rama ${env.BRANCH_NAME}")
    println("El commit ${jenkinsRepoLastCommit[0..7]} del Jenkinsfile se encuentra en la rama ${env.BRANCH_NAME}")

    println("El commit del env ${env.GIT_COMMIT}")
    println("El commit del env ${env.GIT_COMMIT[0..7]}")

    if (jenkinsRepoLastCommit != env.GIT_COMMIT) {
        error "El commit del Jenkinsfile no coincide con el commit del repositorio"
    } else {
        println "El commit del Jenkinsfile coincide con el commit del repositorio"
    }
    sh '/usr/local/bin/docker version'
    // Verificar si la imagen ya existe en EKR
    def imageExists = sh(
        script: "/usr/local/bin/docker manifest inspect ubuntu:20.04 > /dev/null 2>&1 && echo 'true' || echo 'false'",
        returnStdout: true
    ).trim() == 'true'

    if (imageExists) {
        println("La imagen ubuntu:20.04 ya existe en EKR. No se realizará el push.")
    } else {
        println("La imagen ubuntu:20.04 no existe en EKR. Se realizará el push.")
    }
}