pipeline {
    agent any

    environment {
        A="B"
    }

    stages {
        stage('Build') {
            
            environment {
                VERSION="AAA"
            }
            
            agent {
                 docker {
                    image 'golang:1.16-alpine'
                }
            }

            steps {
                echo 'Hello World'
                sh 'echo ${VERSION}'
                sh 'uname -a'

                dir('~') {
                   sh 'pwd'
                   sh 'ls'
                }
                sh 'pwd'
            }
        }

        stage('Test') {

        }
    }
}
