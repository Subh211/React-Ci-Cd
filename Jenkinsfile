pipeline {
    agent any

    environment {
        NODE_ENV = 'test'
    }

    options {
        skipDefaultCheckout(true)
    }

    stages {
        stage ('Code Cleanup') {
            steps {
                cleanWs()
            }
        }

        stage ('Checkout using SCM') {
            steps {
                checkout scm
            }
        }

        stage ('Build') {
            agent {
                docker {
                    image 'node:22.11.0-alpine3.20'
                    args '-u root'
                    reuseNode true
                }
            }

            steps {
                sh '''
                    ls -l
                    node --version
                    npm --version
                    npm install
                    npm run build
                    ls -l 
                '''
            }
        }

        stage ('Test') {
            agent {
                docker {
                     image 'node:22.11.0-alpine3.20'
                     args '-u root'
                     reuseNode true
                }
            }

            steps {
                sh '''
                    npm run test
                '''
            }
        }

        stage ('Deploy') {
            agent {
                docker {
                     image 'node:22.11.0-alpine3.20'
                     args '-u root'
                     reuseNode true
                }
            }

            steps {
                sh '''
                    npm install -g vercel
                    echo NODE_ENV
                '''
            }
        }
    }
}