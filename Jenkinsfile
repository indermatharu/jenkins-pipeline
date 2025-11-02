pipeline {
    agent any

    tools {
        nodejs "node-22.9.0"
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Cleaning workspace...'
                cleanWs()
                echo 'Pulling the React project...'
                git branch: 'main', url: 'https://github.com/indermatharu/jenkins-pipeline.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests with Coverage') {
            steps {
                sh 'npm test -- --coverage'
            }
        }

        stage('Archive Coverage Report') {
            steps {
                script {
                    if (fileExists('coverage/index.html')) {
                        publishHTML(target: [
                            allowMissing: false,
                            keepAll: true,
                            reportDir: 'coverage',
                            reportFiles: 'index.html',
                            reportName: 'Code Coverage Report'
                        ])
                    } else {
                        echo '⚠️ Coverage report not found, skipping publishHTML.'
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }
    }
}
