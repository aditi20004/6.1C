pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo "Building the code"
                bat 'mvn clean package' // Builds the Maven project and packages it
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests"
                bat 'mvn test' // Runs unit tests defined in the Maven project
                junit '**/target/surefire-reports/*.xml' // Publishes JUnit test results
            }
        }
        stage('Code Analysis') {
            steps {
                echo "Running code analysis"
                // Add your static code analysis tool command here, e.g., SonarQube scanner
                bat 'sonar-scanner' // Assuming SonarQube scanner is configured
            }
        }
        stage('Security Scan') {
            steps {
                echo "Performing security scan"
                // Add your security scanning tool command here, e.g., OWASP Dependency Check
                bat 'dependency-check --project "YourProject" --scan "./src" --out "./security-report"'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo "Deploying to staging server"
                // Replace 'deploy-script-command' with your staging deployment script command
                bat 'deploy-to-staging.bat'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on staging"
                // Replace with your integration test command for the staging environment
                bat 'run-integration-tests-staging.bat'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploying to production server"
                // Ensure proper conditions or approvals are in place before deploying to production
                bat 'deploy-to-production.bat'
            }
        }
    }
    post {
        success {
            emailext(
                subject: 'Pipeline Succeeded',
                body: 'The pipeline has completed successfully. You can view the detailed report in the Jenkins dashboard.',
                to: 'shrivastavaditi14@gmail.com'
            )
        }
        failure {
            emailext(
                subject: 'Pipeline Failed',
                body: 'The pipeline has failed. Please check the Jenkins console for more details.',
                to: 'shrivastavaditi14@gmail.com'
            )
        }
    }
}
