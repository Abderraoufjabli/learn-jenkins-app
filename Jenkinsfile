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

<<<<<<< HEAD
        stage('with docker') {
            agent {
                docker {
                    image 'node:22.23.1'
=======
        stage('Build') {
            agent {
                docker {
                    image 'node:22.23.1'
                    reuseNode true
>>>>>>> e160985 (modification jenkinsfile ambiguite entre deux depots)
                }
            }
            steps {
               sh '''
<<<<<<< HEAD
                    echo " ====with docker===="
=======
                    
>>>>>>> e160985 (modification jenkinsfile ambiguite entre deux depots)
                    pwd
                    node -v
                    npm -v 
                    ls -la
<<<<<<< HEAD
                    touch container-yes.txt
=======
                    npm ci
                    npm run build
>>>>>>> e160985 (modification jenkinsfile ambiguite entre deux depots)
                    ls -la
             ''' 
            }
        }
<<<<<<< HEAD
=======

        stage('Test'){
            steps {
                echo 'test stage'
            }
        }
>>>>>>> e160985 (modification jenkinsfile ambiguite entre deux depots)
    }
}