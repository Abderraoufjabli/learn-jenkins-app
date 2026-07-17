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

        stage('with docker') {
            agent {
                docker {
                    image 'node:22.23.1'
                }
            }
            steps {
               sh '''
                    echo " ====with docker===="
                    pwd
                    node -v
                    npm -v 
                    ls -la
                    touch container-yes.txt
                    ls -la
             ''' 
            }
        }
    }
}