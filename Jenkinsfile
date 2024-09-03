pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Building the code"'
                // Use a build automation tool like Maven
                // Example: sh 'mvn clean install'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                sh 'echo "Running unit tests"'
                // Use test automation tools for unit and integration tests
                // Example: sh 'npm test'
            }
        }
        stage('Code Analysis') {
            steps {
                sh 'echo "Running code analysis"'
                // Integrate a code analysis tool
                // Example: sh 'eslint .'
            }
        }
        stage('Security Scan') {
            steps {
                sh 'echo "Performing security scan"'
                // Use a security scanning tool
                // Example: sh 'nmap -p 80 <target>'
            }
        }
        stage('Deploy to Staging') {
            steps {
                sh 'echo "Deploying to staging server"'
                // Deploy to staging server
                // Example: sh 'ssh user@staging-server "deploy-script.sh"'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                sh 'echo "Running integration tests on staging"'
                // Run integration tests on staging
                // Example: sh 'npm run integration-test'
            }
        }
        stage('Deploy to Production') {
            steps {
                sh 'echo "Deploying to production server"'
                // Deploy to production server
                // Example: sh 'ssh user@production-server "deploy-script.sh"'
            }
        }
    }
    post {
        failure {
            emailext(
                subject: 'Pipeline Failed',
                body: 'Pipeline failed. See attached logs for details.',
                attachLog: true,
                to: 'shrivastavaditi14@gmail.com'
            )
        }
        success {
            emailext(
                subject: 'Pipeline Succeeded',
                body: 'Pipeline succeeded. See attached logs for details.',
                attachLog: true,
                to: 'shrivastavaditi14@gmail.com'
            )
        }
    }
}
