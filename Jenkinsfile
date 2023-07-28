pipeline {
    agent any

    stages {
        
        stage('Pre-commit checks') {
            steps {
                // Run your pre-commit checks here, for example:
                sh 'echo "Running pre-commit checks"'
                sh 'pytest' // Run your tests, replace 'pytest' with the actual command to run your tests
                // Add more pre-commit checks as needed
            }
        }
        
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/vastevenson/pytest-intro-vs.git']]])
            }
        }

        stage('Pre-commit Build') {
            steps {
                // Install pre-commit
                sh 'pip install pre-commit'

                // Run pre-commit checks
                //sh 'pre-commit run --all-files'
                sh 'check_added_large_files'
            }
        }
        
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/vastevenson/pytest-intro-vs.git'
                sh 'python3 ops.py'
            }
        }

        stage('Test') {
            steps {
                sh 'python3 -m pytest'
            }
        }
    }
}
