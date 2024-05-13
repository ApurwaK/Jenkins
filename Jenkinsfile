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

                    // Get the list of added or modified files in the latest commit
                    def filesChanged = sh(returnStdout: true, script: 'git diff --name-only HEAD~1 HEAD')
                    
                    // Filter the JSON files among the changed files
                    def jsonFiles = filesChanged.split().findAll { it.endsWith('.json') }

                    // Check indentation for each JSON file
                    for (String file : jsonFiles) {
                        sh "${JSONLINT_HOME}/bin/jsonlint --quiet --indent 4 ${file} || exit 1"
                    }
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
