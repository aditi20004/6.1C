pipeline {
    agent any
    environment {
        STAGING_SERVER = 'staging.example.com'
        PRODUCTION_SERVER = 'production.example.com'
        RECIPIENT_EMAIL = 'shrivastavaditi14@gmail.com'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                // Example: Using Maven as the build tool
                sh 'mvn clean install'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests...'
                // Example: Using JUnit for unit tests and Selenium for integration tests
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code...'
                // Example: Using SonarQube for code quality analysis
                sh 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Example: Using OWASP ZAP for security scans
                sh 'zap-cli quick-scan --self-contained -o http://localhost:8080'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server...'
                // Deployment script or tool command
                sh 'scp -r ./target/myapp.war user@${STAGING_SERVER}:/path/to/deploy'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Use a tool suitable for your environment
                sh 'mvn verify -Denvironment=staging'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server...'
                sh 'scp -r ./target/myapp.war user@${PRODUCTION_SERVER}:/path/to/deploy'
            }
        }
    }
    post {
        always {
            emailext (
                subject: "Jenkins Pipeline Status: ${currentBuild.fullDisplayName}",
                body: """<p>The Jenkins Pipeline ${currentBuild.fullDisplayName} has completed.</p>
                         <p>Status: ${currentBuild.currentResult}</p>
                         <p>Check the build details at: <a href='${BUILD_URL}'>${BUILD_URL}</a></p>""",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                to: "${RECIPIENT_EMAIL}"
            )
        }
    }
}
