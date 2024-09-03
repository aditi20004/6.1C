pipeline {
    agent any

    // Define environment variables
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
                    // Example command to build the application with Maven
                    sh 'mvn clean install'
                    env.BUILD_STATUS = 'SUCCESSFUL'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                script {
                    // Example command to run Maven tests
                    sh 'mvn test'
                    env.TEST_STATUS = 'PASSED'
                }
            }
            post {
                always {
                    echo 'Sending notification email for test stage...'
                    emailext(
                        to: "${env.RECIPIENT_EMAIL}",
                        subject: "Test Stage - ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                        body: """Test stage completed with status: ${env.TEST_STATUS}
                                  Please see attached logs for details.""",
                        attachmentsPattern: "**/target/surefire-reports/*.txt"
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube...'
                script {
                    // Example command to run SonarQube scanner
                    sh 'sonar-scanner'
                    env.CODE_ANALYSIS_STATUS = 'COMPLETED'
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                script {
                    // Example command to run security scan
                    sh 'findsecbugs'
                    env.SECURITY_SCAN_STATUS = 'NO VULNERABILITIES FOUND'
                }
            }
            post {
                always {
                    echo 'Sending notification email for security scan stage...'
                    emailext(
                        to: "${env.RECIPIENT_EMAIL}",
                        subject: "Security Scan Stage - ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                        body: """Security scan stage completed with status: ${env.SECURITY_SCAN_STATUS}
                                  Please see attached logs for details.""",
                        attachmentsPattern: "**/target/findsecbugs-reports/*.txt"
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying to staging server: ${env.STAGING_SERVER}"
                script {
                    // Example command to deploy to the staging server
                    sh "scp target/app.war user@${STAGING_SERVER}:/path/to/deploy"
                    env.STAGING_DEPLOYMENT_STATUS = 'DEPLOYED'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment...'
                script {
                    // Example command for integration tests on staging
                    sh 'remote-integration-test-script.sh'
                    env.STAGING_TESTS_STATUS = 'PASSED'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying to production server: ${env.PRODUCTION_SERVER}"
                script {
                    // Example command to deploy to the production server
                    sh "scp target/app.war user@${PRODUCTION_SERVER}:/path/to/deploy"
                    env.PRODUCTION_DEPLOYMENT_STATUS = 'DEPLOYED'
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
                         See Jenkins for more details."""
            )
        }
    }
}
