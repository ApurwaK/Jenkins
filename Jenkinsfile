pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository from GitHub
                git 'https://github.com/ApurwaK/Jenkins.git'
                echo 'Repository checkout complete.'
            }
        }
        
        stage('Lint JSON files') {
            steps {
                echo 'Linting JSON files...'
                sh 'ls -l' // List files to debug
                sh 'which jsonlint' // Check jsonlint location
                sh 'npm install -g jsonlint' // Install jsonlint
                sh 'jsonlint --version' // Check jsonlint version
                sh 'find . -name "*.json" -exec jsonlint -q --indent 4 {} \\;'
                echo 'JSON linting complete.'
            }
            post {
                success {
                    echo 'JSON indentation check passed!'
                }
                failure {
                    echo 'JSON indentation check failed!'
                    currentBuild.result = 'FAILURE'
                }
            }
        }
    }
}
