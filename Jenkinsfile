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
                    // Placeholder for the build command
                    // Example: sh 'mvn clean install'
                    env.BUILD_STATUS = 'SUCCESSFUL'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                script {
                    // Placeholder for test command
                    // Example: sh 'mvn test'
                    env.TEST_STATUS = 'PASSED'
                }
            }
            post {
                always {
                    script {
                        emailext(
                            to: "${env.RECIPIENT_EMAIL}",
                            subject: "Test Execution - ${currentBuild.fullDisplayName}",
                            body: "Test Execution Status: ${env.TEST_STATUS}",
                            attachmentsPattern: '**/target/surefire-reports/*.xml' // adjust the path according to where your test reports are stored
                        )
                    }
                }
                failure {
                    script {
                        emailext(
                            to: "${env.RECIPIENT_EMAIL}",
                            subject: "Test Execution Failure - ${currentBuild.fullDisplayName}",
                            body: "Test Execution Failed."
                        )
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube...'
                script {
                    // Placeholder for code analysis command
                    // Example: sh 'sonar-scanner'
                    env.CODE_ANALYSIS_STATUS = 'COMPLETED'
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                script {
                    // Placeholder for security scan command
                    // Example: sh 'findsecbugs'
                    env.SECURITY_SCAN_STATUS = 'NO VULNERABILITIES FOUND'
                }
            }
            post {
                always {
                    script {
                        emailext(
                            to: "${env.RECIPIENT_EMAIL}",
                            subject: "Security Scan - ${currentBuild.fullDisplayName}",
                            body: "Security Scan Status: ${env.SECURITY_SCAN_STATUS}",
                            attachmentsPattern: '**/security-reports/*.xml' // adjust the path according to where your security scan reports are stored
                        )
                    }
                }
                failure {
                    script {
                        emailext(
                            to: "${env.RECIPIENT_EMAIL}",
                            subject: "Security Scan Failure - ${currentBuild.fullDisplayName}",
                            body: "Security Scan Failed."
                        )
                    }
                }
            }
        }

        // Other stages...

    }

    post {
        always {
            echo 'Sending final notification email...'
            mail to: "${env.RECIPIENT_EMAIL}",
                 subject: "Build ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                 body: """Pipeline execution details:
                          Build Status: ${env.BUILD_STATUS}
                          Test Status: ${env.TEST_STATUS}
                          Code Analysis Status: ${env.CODE_ANALYSIS_STATUS}
                          Security Scan Status: ${env.SECURITY_SCAN_STATUS}
                          See Jenkins for more details."""
        }
    }
}
