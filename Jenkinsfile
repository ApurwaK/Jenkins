pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository from GitHub
                git 'https://github.com/ApurwaK/Jenkins.git'
            }
        }
        stage('Lint JSON Files') {
            steps {
                script {
                    // Install jsonlint tool if not installed already
                    tool name: 'jsonlint', type: 'com.cloudbees.jenkins.plugins.customtools.CustomToolInstallation'
                    
                    // Find JSON files and check their indentation
                    sh 'find . -name "*.json" -exec ${JSONLINT_HOME}/bin/jsonlint --quiet --indent 4 {} \\; || exit 1'
                }
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
