pipeline {
    agent any

    stages {

        stage('Without Docker') {
            steps {
                sh '''
                    echo "==== Without Docker ===="
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

                    echo "=== Build generated ==="
                    ls -la
                    ls -la build

                    test -f build/index.html
                '''
            }
        }

        stage('Test') {
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
                    npm test
                '''
            }
        }

        stage('E2E') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }

            environment {
                HOME = "${WORKSPACE}"
                NPM_CONFIG_CACHE = "${WORKSPACE}/.npm"
            }

            steps {
                sh '''
                    test -f build/index.html

                    npm ci

                    echo "Starting web server..."
                    npx serve -s build -l 3000 &

                    sleep 5

                    curl http://localhost:3000

                    echo "Running Playwright tests..."
                    npx playwright test
                '''
            }
        }
    }

    post {
        always {
            echo "Pipeline finished."
        }

        success {
            echo "Build succeeded."
        }

        failure {
            echo "Build failed."
        }
    }
}