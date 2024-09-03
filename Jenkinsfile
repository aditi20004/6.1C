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
                bat 'mvn clean install' // Using bat for Windows
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests...'
                bat 'mvn test' // Using bat for Windows
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code...'
                bat 'mvn sonar:sonar' // Using bat for Windows, ensure SonarQube is configured properly
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // For Windows, you might need a different command or tool that can be run directly or through a script
                echo 'Security scanning tools need to be configured for Windows'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server...'
                // Implement deployment via scripts or tools that work on Windows
                echo 'Deploy script or tool needs to be configured for Windows'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                bat 'mvn verify -Denvironment=staging' // Using bat for Windows
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server...'
                // Implement deployment via scripts or tools that work on Windows
                echo 'Deploy script or tool needs to be configured for Windows'
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
