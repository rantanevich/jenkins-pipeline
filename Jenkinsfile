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
                echo 'prepares something...'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run -it --entrypoint "" alpine/helm:3.5.4 helm version' 
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
