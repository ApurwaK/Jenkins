pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout your repository from GitHub
                git 'https://github.com/ApurwaK/Jenkins.git'
            }
        }
        stage('Lint JSON files') {
            steps {
                // Install any necessary dependencies
                sh 'npm install -g jsonlint'
                
                // Run jsonlint command to check indentation
                sh 'jsonlint --quiet --indent 4 *.json || exit 1'
            }
            post {
                failure {
                    // If indentation check fails, print an error message and exit with error status
                    echo 'JSON indentation check failed!'
                    error 'JSON indentation check failed!'
                }
            }
        }
    }
}
