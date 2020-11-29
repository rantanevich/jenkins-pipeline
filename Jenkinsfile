pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    environment {
        OWNER = 'rantanevich'
        REPOSITORY = 'jenkins-pipeline'
        GITHUB_TOKEN = credentials('GITHUB_TOKEN')
    }

    stages {
        stage('Prepare') {
            steps {
                sh 'export'
                sh 'ls -la'
                echo 'prepares something...'
            }
        }
        stage('Test') {
            steps {
                echo 'tests something...'
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

    post {
        success {
            sh '''curl "https://api.github.com/repos/${OWNER}/${REPOSITORY}/statuses/${GIT_COMMIT}" \
                        -H "Authorization: token ${GITHUB_TOKEN}" \
                        -H "Content-Type: application/json" \
                        -X POST \
                        -d "{\\\"state\\\": \\\"success\\\",\\\"context\\\": \\\"continuous-integration/jenkins\\\", \\\"description\\\": \\\"Jenkins\\\", \\\"target_url\\\": \\\"${BUILD_URL}/console\\\"}"
            '''
        }
        failure {
            sh '''curl "https://api.github.com/repos/${OWNER}/${REPOSITORY}/statuses/${GIT_COMMIT}" \
                        -H "Authorization: token ${GITHUB_TOKEN}" \
                        -H "Content-Type: application/json" \
                        -X POST \
                        -d "{\\\"state\\\": \\\"failure\\\",\\\"context\\\": \\\"continuous-integration/jenkins\\\", \\\"description\\\": \\\"Jenkins\\\", \\\"target_url\\\": \\\"${BUILD_URL}/console\\\"}"
            '''
        }
    }
}