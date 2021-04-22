pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    stages {
        stage('Prepare') {
            steps {
                sh 'printenv'
                sh 'ls -la'
                echo 'hello from ${GIT_BRANCH} branch'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run --rm alpine/helm:3.5.4 version' 
            }
        }
        stage('Production') {
            when {
                branch 'main'
            }
            stages {
                stage('Build') {
                    steps {
                        echo 'builds something...'
                    }
                }
                stage('Push') {
                    steps {
                        echo 'pushes something...'
                    }
                }
                stage('Deploy to stage') {
                    steps {
                        echo 'deploys something to stage...'
                    }
                }
                stage('Approval') {
                    steps {
                        echo 'approval something...'
                    }
                }
                stage('Deploy to production') {
                    steps {
                        echo 'deploys something to production...'
                    }
                }
            }
        }
    }
}
