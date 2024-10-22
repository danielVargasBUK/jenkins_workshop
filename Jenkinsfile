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
        stage('ArgoCD sync') {
            steps {
                script {
                    try {
                        timeout(time: 1, unit: 'MINUTES') {
                            echo "timeout step"
                                sh """
                                export PATH=$PATH:/opt/homebrew/bin/argocd
                                argocd app terminate-op app-2 --http-retry-max 50 --grpc-web --loglevel debug --server 127.0.0.1:8000 ||  true
                                argocd app sync app-2 --http-retry-max 50 --grpc-web --loglevel debug --server 127.0.0.1:8000 --timeout 14400
                                argocd app wait app-2 --http-retry-max 50 --grpc-web --loglevel debug --health --server 127.0.0.1:8000
                                """
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