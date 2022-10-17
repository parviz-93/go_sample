pipeline {
    
    agent any

    tools {
        go 'go_1.16'
    }

    stages {
        stage('Build') {
            
            environment {
                VERSION="AAA"
            }
            
            steps {
                sh 'go mod download'
                sh 'go build -v ./...'
            }
        }

        stage('Test') {
            when {
                expression {
                    return params.SKIP_TEST == true;
                }
            }
        
            steps {
                sh 'go test -v ./...'
            }
        }

        stage('Build image') {
            steps {
               sh 'go test -v ./...'
            }
        }

    }
}
