pipeline {
    agent {
        docker {
            image 'alpine:3.13.2'
        }
    }

    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    stages {
        stage('Prepare') {
            steps {
                sh 'printenv'
                sh 'ls -lha'
                echo "hello from ${GIT_BRANCH} branch"
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'alpine/helm:3.5.4'
                    args '--entrypoint=/bin/sh'
                }
            }
            steps {
		sh 'echo Test stage'
                sh 'helm version'
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
