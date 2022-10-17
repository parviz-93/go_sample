pipeline {
    
    agent any

    triggers {
        cron('H */2 * * *')
        pollSCM('H/5 * * * *')
    }

    parameters {
        string(name: 'TAG', defaultValue: "latest")
        booleanParam(name: 'SKIP_TEST', defaultValue: false)
        booleanParam(name: 'SKIP_PUBLISH_IMAGE', defaultValue: false)
    }

    tools {
        go 'go_1.16'
        git 'Default'
    }

    stages {
        stage('Build') {
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
              sh ('docker build -t rozikovp/go-sample:${TAG} .')
            }
        }

        stage('Publish image') {
            when {
                expression {
                    return params.SKIP_PUBLISH_IMAGE == false;
                }
            }

            steps{
               withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                    sh('docker login -u ${dockerHubUser} -p ${dockerHubPassword}')
                    sh('docker push rozikovp/go-sample:${TAG}')
                }
            }
        }

        stage("Push tag to git") {
            when {
                expression {
                    return params.SKIP_PUBLISH_IMAGE == false;
                }
            }

            steps {
                sh("git config user.name 'Jenkins'")
                sh("git config user.email 'jenkins@mycompany.com'")

                withCredentials([gitUsernamePassword(credentialsId: 'github-parviz-token',gitToolName: 'git-tool')]) {
                        sh('git tag ${TAG}')
                        sh('git push --tags')
                }
            }

        }
    }
}
