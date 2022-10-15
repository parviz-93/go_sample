pipeline {
    agent any

    enviroment {

    }
    
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                sh 'echo 1'
                sh 'uname -a'

                dir('~') {
                   sh 'pwd'
                   sh 'ls'
                }
                sh 'pwd'
            }
        }
    }
}
