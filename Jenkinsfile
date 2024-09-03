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
                echo 'Building the application using Maven...'
                script {
                    // Example: sh 'mvn clean install'
                    env.BUILD_STATUS = 'SUCCESSFUL' // Modify this based on actual build outcome
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                script {
                    // Example: sh 'mvn test'
                    env.TEST_STATUS = 'PASSED' // Modify this based on actual test outcomes
                }
            }
            post {
                always {
                    echo 'Sending notification email for test stage...'
                    emailext(
                        to: "${env.RECIPIENT_EMAIL}",
                        subject: "Test Stage - ${currentBuild.fullDisplayName} - ${env.TEST_STATUS}",
                        body: """Test stage completed with status: ${env.TEST_STATUS}.
                                  Please see attached logs for details.""",
                        attachLog: true,
                        compressLog: true
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube...'
                script {
                    // Example: sh 'sonar-scanner'
                    env.CODE_ANALYSIS_STATUS = 'COMPLETED' // Adjust based on actual results
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                script {
                    // Example: sh 'findsecbugs'
                    env.SECURITY_SCAN_STATUS = 'NO VULNERABILITIES FOUND' // Adjust accordingly
                }
            }
            post {
                always {
                    echo 'Sending notification email for security scan stage...'
                    emailext(
                        to: "${env.RECIPIENT_EMAIL}",
                        subject: "Security Scan Stage - ${currentBuild.fullDisplayName} - ${env.SECURITY_SCAN_STATUS}",
                        body: """Security scan stage completed with status: ${env.SECURITY_SCAN_STATUS}.
                                  Please see attached logs for details.""",
                        attachLog: true,
                        compressLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying to staging server: ${env.STAGING_SERVER}"
                script {
                    // Example: sh 'scp target/app.war user@${STAGING_SERVER}:/path/to/deploy'
                    env.STAGING_DEPLOYMENT_STATUS = 'DEPLOYED' // Adjust based on outcome
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment...'
                script {
                    // Example: sh 'remote-integration-test-script.sh'
                    env.STAGING_TESTS_STATUS = 'PASSED' // Modify based on test results
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying to production server: ${env.PRODUCTION_SERVER}"
                script {
                    // Example: sh 'scp target/app.war user@${PRODUCTION_SERVER}:/path/to/deploy'
                    env.PRODUCTION_DEPLOYMENT_STATUS = 'DEPLOYED' // Adjust based on outcome
                }
            }
        }
    }

    post {
        always {
            echo 'Sending final notification email...'
            emailext(
                to: "${env.RECIPIENT_EMAIL}",
                subject: "Build ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                body: """Pipeline execution details:
                         Build Status: ${env.BUILD_STATUS}
                         Test Status: ${env.TEST_STATUS}
                         Code Analysis Status: ${env.CODE_ANALYSIS_STATUS}
                         Security Scan Status: ${env.SECURITY_SCAN_STATUS}
                         Staging Deployment Status: ${env.STAGING_DEPLOYMENT_STATUS}
                         Staging Tests Status: ${env.STAGING_TESTS_STATUS}
                         Production Deployment Status: ${env.PRODUCTION_DEPLOYMENT_STATUS}
                         See Jenkins for more details.""",
                attachLog: true,
                compressLog: true
            )
        }
    }
}
