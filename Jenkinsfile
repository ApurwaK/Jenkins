pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository from GitHub
                git 'https://github.com/ApurwaK/Jenkins.git'
            }
        }
        stage('Lint JSON files') {
            steps {
                // Install any necessary dependencies (e.g., jq for JSON parsing)
                sh 'apt-get update && apt-get install -y jq'
                
                // Find JSON files and check indentation
                script {
                    def jsonFiles = sh(script: "git ls-files '*.json'", returnStdout: true).trim().split('\n')
                    for (def file in jsonFiles) {
                        def indentation = sh(script: "jq --indent 0 . $file | wc -l | xargs", returnStdout: true).trim().toInteger()
                        if (indentation % 4 != 0) {
                            error "Indentation error in file: $file"
                        }
                    }
                }
            }
        }
    }
}
