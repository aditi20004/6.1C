pipeline {
    agent any

    stages {
        // Stage 1: Build
        stage('Build') {
            steps {
                script {
                    // Maven is used for Java projects
                    sh 'mvn clean install'
                }
            }
        }

        // Stage 2: Unit and Integration Tests
        stage('Unit and Integration Tests') {
            steps {
                script {
                    // Example: Using JUnit for Java projects and integrating with Jenkins
                    sh 'mvn test'
                }
            }
        }

        // Stage 3: Code Analysis
        stage('Code Analysis') {
            steps {
                script {
                    // Example: Using SonarQube for code quality analysis
                    sh 'mvn sonar:sonar'
                }
            }
        }

        // Stage 4: Security Scan
        stage('Security Scan') {
            steps {
                script {
                    // Example: Using OWASP ZAP for security scanning
                    sh 'zap-cli quick-scan --self-contained --start-options "-config api.disablekey=true" http://localhost:8080'
                }
            }
        }

        // Stage 5: Deploy to Staging
        stage('Deploy to Staging') {
            steps {
                script {
                    // Deploy to a staging server
                    sh 'ssh user@staging-server "deploy-script.sh"'
                }
            }
        }

        // Stage 6: Integration Tests on Staging
        stage('Integration Tests on Staging') {
            steps {
                script {
                    // Run integration tests on the staging environment
                    sh 'mvn verify -Pintegration-tests'
                }
            }
        }

        // Stage 7: Deploy to Production
        stage('Deploy to Production') {
            steps {
                script {
                    // Deploy to a production server
                    sh 'ssh user@production-server "deploy-script.sh"'
                }
            }
        }
    }

    post {
        // Send notification emails after test and security scan stages
        always {
            // Adjust as needed to target specific stages if conditional emailing is desired
            emailext(
                subject: 'Jenkins Pipeline ${STAGE_NAME} Status: ${BUILD_STATUS}',
                body: '''<p>Pipeline ${BUILD_STATUS} for ${STAGE_NAME}.</p>
                         <p>See attached logs for details.</p>''',
                attachLog: true,
                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                to: 'shrivastavaditi14@gmail.com'
            )
        }
    }
}
