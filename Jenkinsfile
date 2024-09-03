pipeline {
    agent any

    environment {
        // Define the recipient email
        RECIPIENT_EMAIL = 'shrivastavaditi14@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Assuming Maven as the build tool
                    sh 'mvn clean package'
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                script {
                    // Example: Run tests with Maven
                    sh 'mvn test'
                }
            }
            post {
                always {
                    script {
                        def status = currentBuild.result ?: 'SUCCESS'
                        def emailBody = """
                            The Test stage completed with status: ${status}
                            Build details at: ${env.BUILD_URL}
                        """
                        // Send an email notification with logs
                        emailext(
                            to: "${env.RECIPIENT_EMAIL}",
                            subject: "Jenkins Notification: Test Stage - ${status}",
                            body: emailBody,
                            attachLog: true
                        )
                    }
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                script {
                    // Example: Using SonarQube for code analysis
                    sh 'mvn sonar:sonar'
                }
            }
        }
        
        stage('Security Scan') {
            steps {
                script {
                    // Placeholder for security scan tool command
                    echo 'Performing security scan...'
                }
            }
            post {
                always {
                    script {
                        def status = currentBuild.result ?: 'SUCCESS'
                        def emailBody = """
                            The Security Scan stage completed with status: ${status}
                            Build details at: ${env.BUILD_URL}
                        """
                        // Send an email notification with logs
                        emailext(
                            to: "${env.RECIPIENT_EMAIL}",
                            subject: "Jenkins Notification: Security Scan - ${status}",
                            body: emailBody,
                            attachLog: true
                        )
                    }
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                script {
                    // Placeholder for deployment command
                    echo 'Deploying to staging environment...'
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                script {
                    // Placeholder for integration testing command
                    echo 'Running integration tests on staging...'
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                script {
                    // Placeholder for production deployment command
                    echo 'Deploying to production environment...'
                }
            }
        }
    }
    
    post {
        always {
            // Archive logs and other artifacts
            archiveArtifacts artifacts: '**/target/*.log', fingerprint: true
        }
    }
}
