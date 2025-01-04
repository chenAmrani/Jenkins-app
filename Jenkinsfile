pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine' //the workspace with Node18
                    reuseNode true //save the files to be availiable in the container
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine' //the workspace with Node18
                    reuseNode true //save the files to be availiable in the container
                }
            }
            steps {
            sh '''
                echo "Test stage"
                test build/index.html
                npm test
            '''
            }
        }   

        stage('E2E') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.49.1-noble' 
                    reuseNode true 
                }
            }
            steps {
            sh '''
                npm install serve
                node_modules/.bin/serve -s build &
                sleep 50
                npx playwirght test show-report
            '''
            }
        } 
    }

    post {
        always {
            junit 'jest-results/junit.xml'
        }
    }
}