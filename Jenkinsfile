pipeline {
    agent any

    stages {
        stage('w/o docker') {
            steps {
                sh '''
                   echo "==== without docker===="
                   pwd
                   ls -la 
                   touch container-no.txt
                   ls -la
                ''' 
            }
        }

        stage('Build') {
            agent {
                docker {
                    image 'node:22.23.1'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    pwd
                    node -v
                    npm -v 
                    ls -la
                    npm ci
                    npm run build
                    ls -la
                ''' 
            }
        }

        stage('Test'){
            steps {
                echo 'test stage'
            }
        }
    }
}