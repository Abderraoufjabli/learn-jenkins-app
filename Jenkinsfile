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
            environment {
        HOME = "${WORKSPACE}"
        NPM_CONFIG_CACHE = "${WORKSPACE}/.npm"
    }
            steps {
                sh '''
                    echo "HOME=$HOME"
                    rm -rf node_modules
                    rm -rf build
                    node -v
                    npm -v
                    npm ci
                    npm run build
                    ls -la
                ''' 
            }
        }

        stage('Test'){
             docker {
                    image 'node:22.23.1'
                    reuseNode true
                }

            steps {
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }
    }
}

