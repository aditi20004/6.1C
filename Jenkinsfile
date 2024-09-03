pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo "Building the code"
                // Use a build automation tool like Maven
                // Example: bat 'mvn clean install'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests"
                // Use test automation tools for unit and integration tests
                // Example: bat 'npm test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo "Running code analysis"
                // Integrate a code analysis tool
                // Example: bat 'eslint .'
            }
        }
        stage('Security Scan') {
            steps {
                echo "Performing security scan"
                // Use a security scanning tool
                // Example: bat 'nmap -p 80 <target>'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo "Deploying to staging server"
                // Deploy to staging server
                // Example: bat 'ssh user@staging-server "deploy-script.sh"'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on staging"
                // Run integration tests on staging
                // Example: bat 'npm run integration-test'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploying to production server"
                // Deploy to production server
                // Example: bat 'ssh user@production-server "deploy-script.sh"'
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
