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
                    sh 'echo "Building the application" > ${LOG_DIR}/build.log'
                    // Example: sh 'mvn clean install >> ${LOG_DIR}/build.log 2>&1'
                    env.BUILD_STATUS = 'SUCCESSFUL' // Modify this based on actual build outcome
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                script {
                    sh 'echo "Running unit and integration tests" > ${LOG_DIR}/unit_integration_tests.log'
                    // Example: sh 'mvn test >> ${LOG_DIR}/unit_integration_tests.log 2>&1'
                    env.TEST_STATUS = 'PASSED' // Modify this based on actual test outcomes
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube...'
                script {
                    sh 'echo "Analyzing code" > ${LOG_DIR}/code_analysis.log'
                    // Example: sh 'sonar-scanner >> ${LOG_DIR}/code_analysis.log 2>&1'
                    env.CODE_ANALYSIS_STATUS = 'COMPLETED' // Adjust based on actual results
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                script {
                    sh 'echo "Performing security scan" > ${LOG_DIR}/security_scan.log'
                    // Example: sh 'findsecbugs >> ${LOG_DIR}/security_scan.log 2>&1'
                    env.SECURITY_SCAN_STATUS = 'NO VULNERABILITIES FOUND' // Adjust accordingly
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying to staging server: ${env.STAGING_SERVER}"
                script {
                    sh 'echo "Deploying to staging" > ${LOG_DIR}/staging_deploy.log'
                    // Example: sh 'scp target/app.war user@${STAGING_SERVER}:/path/to/deploy >> ${LOG_DIR}/staging_deploy.log 2>&1'
                    env.STAGING_DEPLOYMENT_STATUS = 'DEPLOYED' // Adjust based on outcome
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment...'
                script {
                    sh 'echo "Running integration tests on staging" > ${LOG_DIR}/staging_tests.log'
                    // Example: sh 'remote-integration-test-script.sh >> ${LOG_DIR}/staging_tests.log 2>&1'
                    env.STAGING_TESTS_STATUS = 'PASSED' // Modify based on test results
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying to production server: ${env.PRODUCTION_SERVER}"
                script {
                    sh 'echo "Deploying to production" > ${LOG_DIR}/production_deploy.log'
                    // Example: sh 'scp target/app.war user@${PRODUCTION_SERVER}:/path/to/deploy >> ${LOG_DIR}/production_deploy.log 2>&1'
                    env.PRODUCTION_DEPLOYMENT_STATUS = 'DEPLOYED' // Adjust based on outcome
                }
            }
        }
    }

    post {
        always {
            // Sending final summary email without attachments
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

            // Sending an email with logs as attachments
            echo 'Sending email with logs attached...'
            emailext attachmentsPattern: "${env.LOG_DIR}/*.log",
                     to: "${env.RECIPIENT_EMAIL}",
                     subject: "Pipeline Logs for ${currentBuild.fullDisplayName}",
                     body: "Please find the logs from the pipeline execution attached."
        }
    }
}
