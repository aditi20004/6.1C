pipeline {
    agent any

    // Define environment variables
    environment {
        STAGING_SERVER = 'staging.example.com'
        PRODUCTION_SERVER = 'production.example.com'
        RECIPIENT_EMAIL = 'shrivastavaditi14@gmail.com'
        LOG_PATH = 'logs' // Define the path where logs should be stored
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven...'
                // Placeholder for actual build command
                // Example: sh 'mvn clean install > ${LOG_PATH}/build.log'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                script {
                    // Placeholder for test command
                    // Example: sh 'mvn test > ${LOG_PATH}/test.log'
                    env.TEST_STATUS = 'PASSED' // Adjust based on actual results
                }
            }
            post {
                always {
                    echo 'Sending email notification for testing stage...'
                    emailext to: "${env.RECIPIENT_EMAIL}",
                              subject: "Testing Stage - ${env.TEST_STATUS}",
                              body: "The testing stage has ${env.TEST_STATUS}. Please find the logs attached.",
                              attachmentsPattern: "${LOG_PATH}/test.log"
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube...'
                // Placeholder for code analysis command
                // Example: sh 'sonar-scanner > ${LOG_PATH}/code_analysis.log'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                script {
                    // Placeholder for security scan command
                    // Example: sh 'findsecbugs > ${LOG_PATH}/security_scan.log'
                    env.SECURITY_STATUS = 'NO VULNERABILITIES FOUND' // Adjust accordingly
                }
            }
            post {
                always {
                    echo 'Sending email notification for security scan stage...'
                    emailext to: "${env.RECIPIENT_EMAIL}",
                              subject: "Security Scan Stage - ${env.SECURITY_STATUS}",
                              body: "The security scan stage has ${env.SECURITY_STATUS}. Please find the logs attached.",
                              attachmentsPattern: "${LOG_PATH}/security_scan.log"
                }
            }
        }

        // Other stages...

        stage('Deploy to Production') {
            steps {
                echo "Deploying to production server: ${env.PRODUCTION_SERVER}"
                // Placeholder for deployment command
                // Example: sh 'scp target/app.war user@${PRODUCTION_SERVER}:/path/to/deploy'
            }
        }
    }
}
