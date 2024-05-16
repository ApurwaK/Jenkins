pipeline {
    agent any
    
    tools {
        nodejs 'Recent node' // Use the NodeJS installation configured in Jenkins
    }
    
    stages {
        stage('Checkout') {
            steps {
                git  'https://github.com/ApurwaK/Jenkins.git'
            }
        }
        stage('Install JSONLint') {
            steps {
                // JSONLint should already be installed globally, so this step is just for demonstration
                // sh 'npm install -g jsonlint' // This line can be omitted if configured globally
                echo 'JSONLint is assumed to be installed globally'
            }
        }
        stage('Lint JSON files') {
            steps {
                // Run jsonlint command to check indentation
                sh 'find . -name "*.json" -exec jsonlint --quiet --indent 4 {} \\;'
            }
            post {
                failure {
                    echo 'JSON indentation check failed!'
                    error 'JSON indentation check failed!'
                }
            }
        }
    }
}
