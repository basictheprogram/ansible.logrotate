pipeline {
    agent {
        label '!windows'
    }

    stages {
        stage('Check out the codebase') {
            agent any
            steps {
                ws('basictheprogram.terraria_server')  {
                    checkout scm
                }
            }
        }
        stage('Install test dependencies') {
            agent any
            steps {
                sh 'pip3 install molecule docker yamllint ansible-lint'
            }
        }
        stage('Run molecule tests') {
            agent any
            
            environment {
                PATH       = "/var/jenkins/.local/bin:${PATH}"
                PYTHONPATH = "${WORKSPACE}"
            }
            
            steps {
                ws('basictheprogram.terraria_server')  {
                    sh 'molecule test'
                }
            }
            post {
                always {
                    echo 'One way or another, I have finished'
                    cleanWs()
                }
            }
        }
    }
}
