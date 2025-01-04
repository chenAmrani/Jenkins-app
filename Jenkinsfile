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
            steps {
            sh '''
                echo"Test stage"
            '''
            }
        }    
    }
}