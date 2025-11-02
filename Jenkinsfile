pipeline {
    agent any

    tools {
        nodejs "node-22.9.0"
    }

    environment {
        COVERAGE_DIR = "coverage"
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Pulling the git project'
                git branch: 'main', url: 'https://github.com/indermatharu/jenkins-pipeline.git'
            }
        }

        stage('Install dependencies') {
            steps {
                echo 'Installing....'
                sh 'npm install'
            }
        }

        stage('Run tests with coverage') {
            steps {
                echo 'Generating code coverage report...'
                sh 'npm test -- --coverage'
            }
        }

        stage('Archive coverage report') {
            steps {
                publishHTML(target: [
                    allowMissing: false,
                    keepAll: true,
                    reportDir: "${COVERAGE_DIR}/lcov-report",
                    reportFiles: 'index.html',
                    reportName: 'Code coverage report'
                ])
            }
        }
    }
}
