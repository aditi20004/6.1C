pipeline {
    agent any
    tools {
        // Ensure the name 'Maven' matches exactly with the name configured in Jenkins
        maven 'Maven'
    }
    environment {
        STAGING_SERVER = 'staging.example.com'
        PRODUCTION_SERVER = 'production.example.com'
        RECIPIENT_EMAIL = 'shrivastavaditi14@gmail.com'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                bat 'mvn clean install' // Use 'bat' on Windows
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests...'
                bat 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code...'
                bat 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // You need to specify your security scanning tools or commands here
                echo 'Placeholder for security scanning tools or commands'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server...'
                // Replace this echo with actual deployment commands or scripts
                echo 'Placeholder for deployment commands or scripts'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                bat 'mvn verify -Denvironment=staging'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server...'
                // Replace this echo with actual deployment commands or scripts
                echo 'Placeholder for deployment commands or scripts'
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
                to: "${RECIPIENT_EMAIL}"
            )
        }
    }
}
