pipeline {
    agent any

    // Define environment variables
    environment {
        STAGING_SERVER = 'staging.example.com'
        PRODUCTION_SERVER = 'production.example.com'
        RECIPIENT_EMAIL = 'shrivastavaditi14@gmail.com'
        LOG_DIR = 'logs'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven...'
                script {
                    // Placeholder for the build command
                    // Example: sh 'mvn clean install'
                    env.BUILD_STATUS = 'SUCCESSFUL' // Modify this based on actual build outcome
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                script {
                    // Placeholder for test command
                    // Example: sh 'mvn test > ${env.LOG_DIR}/unit_integration_tests.log'
                    env.TEST_STATUS = 'PASSED' // Modify this based on actual test outcomes
                }
            }
            post {
                always {
                    // Send email notification with logs
                    echo 'Sending email with logs for Unit and Integration Tests...'
                    emailext attachmentsPattern: "${env.LOG_DIR}/unit_integration_tests.log",
                             to: "${env.RECIPIENT_EMAIL}",
                             subject: "Unit and Integration Tests - ${env.TEST_STATUS}",
                             body: "The Unit and Integration Tests have ${env.TEST_STATUS}. Please find the logs attached."
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube...'
                script {
                    // Placeholder for code analysis command
                    // Example: sh 'sonar-scanner'
                    env.CODE_ANALYSIS_STATUS = 'COMPLETED' // Adjust based on actual results
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                script {
                    // Placeholder for security scan command
                    // Example: sh 'findsecbugs > ${env.LOG_DIR}/security_scan.log'
                    env.SECURITY_SCAN_STATUS = 'NO VULNERABILITIES FOUND' // Adjust accordingly
                }
            }
            post {
                always {
                    // Send email notification with logs
                    echo 'Sending email with logs for Security Scan...'
                    emailext attachmentsPattern: "${env.LOG_DIR}/security_scan.log",
                             to: "${env.RECIPIENT_EMAIL}",
                             subject: "Security Scan - ${env.SECURITY_SCAN_STATUS}",
                             body: "The Security Scan has completed with status: ${env.SECURITY_SCAN_STATUS}. Please find the logs attached."
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying to staging server: ${env.STAGING_SERVER}"
                script {
                    // Placeholder for deployment command
                    // Example: sh 'scp target/app.war user@${STAGING_SERVER}:/path/to/deploy'
                    env.STAGING_DEPLOYMENT_STATUS = 'DEPLOYED' // Adjust based on outcome
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment...'
                script {
                    // Placeholder for integration tests on staging
                    // Example: sh 'remote-integration-test-script.sh'
                    env.STAGING_TESTS_STATUS = 'PASSED' // Modify based on test results
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying to production server: ${env.PRODUCTION_SERVER}"
                script {
                    // Placeholder for deployment command
                    // Example: sh 'scp target/app.war user@${PRODUCTION_SERVER}:/path/to/deploy'
                    env.PRODUCTION_DEPLOYMENT_STATUS = 'DEPLOYED' // Adjust based on outcome
                }
            }
        }
    }

    post {
        always {
            echo 'Sending final summary email...'
            mail to: "${env.RECIPIENT_EMAIL}",
                 subject: "Build ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                 body: """Pipeline execution details:
                          Build Status: ${env.BUILD_STATUS}
                          Test Status: ${env.TEST_STATUS}
                          Code Analysis Status: ${env.CODE_ANALYSIS_STATUS}
                          Security Scan Status: ${env.SECURITY_SCAN_STATUS}
                          Staging Deployment Status: ${env.STAGING_DEPLOYMENT_STATUS}
                          Staging Tests Status: ${env.STAGING_TESTS_STATUS}
                          Production Deployment Status: ${env.PRODUCTION_DEPLOYMENT_STATUS}
                          See Jenkins for more details."""
        }
    }
}
