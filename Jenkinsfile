pipeline {
    
    agent any

    triggers {
        cron('H */2 * * *')
        pollSCM('H/5 * * * *')
    }

    parameters {
        booleanParam(name: 'SKIP_TEST', defaultValue: false)
        booleanParam(name: 'SKIP_PUBLISH_IMAGE', defaultValue: false)
    }

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
                    return params.SKIP_TEST == false;
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
