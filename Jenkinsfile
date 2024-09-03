pipeline {
    agent any

    environment {
        // Define environment variables for servers and email recipient
        STAGING_SERVER = 'staging.example.com'
        PRODUCTION_SERVER = 'production.example.com'
        RECIPIENT_EMAIL = 'shrivastavaditi14@gmail.com'
        LOG_PATH = 'logs' // Directory to store logs
    }

    tools {
        // Specify any tools needed, like Maven or Gradle if used
        maven 'Maven 3.6.3' // Adjust the version as per your configuration
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven...'
                sh 'mvn clean package > ${LOG_PATH}/build.log' // Adjust the command as necessary
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                script {
                    sh 'mvn test > ${LOG_PATH}/test.log' // Adjust the command as necessary
                    env.TEST_STATUS = 'PASSED' // This should be dynamically set based on actual test results
                }
            }
            post {
                always {
                    emailext (
                        to: "${env.RECIPIENT_EMAIL}",
                        subject: "Testing Stage - ${env.TEST_STATUS}",
                        body: "The testing stage has ${env.TEST_STATUS}. Please find the logs attached.",
                        attachmentsPattern: "${LOG_PATH}/test.log",
                        mimeType: 'text/html'
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube...'
                sh 'sonar-scanner > ${LOG_PATH}/code_analysis.log' // Adjust the command as necessary
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                script {
                    sh 'findsecbugs > ${LOG_PATH}/security_scan.log' // Adjust the command as necessary
                    env.SECURITY_STATUS = 'NO VULNERABILITIES FOUND' // This should be dynamically set based on actual scan results
                }
            }
            post {
                always {
                    emailext (
                        to: "${env.RECIPIENT_EMAIL}",
                        subject: "Security Scan Stage - ${env.SECURITY_STATUS}",
                        body: "The security scan stage has ${env.SECURITY_STATUS}. Please find the logs attached.",
                        attachmentsPattern: "${LOG_PATH}/security_scan.log",
                        mimeType: 'text/html'
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying to staging server: ${env.STAGING_SERVER}"
                sh 'scp target/app.war user@${STAGING_SERVER}:/path/to/deploy' // Adjust the command as necessary
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment...'
                sh 'remote-integration-test-script.sh > ${LOG_PATH}/staging_test.log' // Adjust the command as necessary
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying to production server: ${env.PRODUCTION_SERVER}"
                sh 'scp target/app.war user@${PRODUCTION_SERVER}:/path/to/deploy' // Adjust the command as necessary
            }
        }
    }

    post {
        failure {
            emailext (
                to: "${env.RECIPIENT_EMAIL}",
                subject: "Pipeline Failure - ${currentBuild.fullDisplayName}",
                body: "A failure occurred in the Jenkins Pipeline. Please check Jenkins for more details.",
                mimeType: 'text/html'
            )
        }
    }
}
