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
                // Conditional execution based on operating system
                script {
                    if (isUnix()) {
                        // Unix-specific command to find and lint JSON files
                        sh 'find . -name "*.json" -exec jsonlint --quiet --indent 4 {} \\;'
                    } else {
                        // Windows-specific command to find and lint JSON files
                        bat '''
                        for /R %%i in (*.json) do (
                            jsonlint --quiet --indent 4 "%%i" || exit /b 1
                        )
                        '''
                    }
                }
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
