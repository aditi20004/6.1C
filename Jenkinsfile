pipeline {
    agent any

    environment {
        // Define the recipient email
        RECIPIENT_EMAIL = 'shrivastavaditi14@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                // Example build step
                echo 'Building...'
                // Use your build tools here e.g., Maven
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                // Example test execution step
                echo 'Running tests...'
                // Use your test automation tools here
            }
            post {
                always {
                    // Send an email notification with logs
                    emailext (
                        to: "${env.RECIPIENT_EMAIL}",
                        subject: "Jenkins Notification: Test Stage Completed",
                        body: "The test stage has ${currentBuild.currentResult}: Check console output at ${env.BUILD_URL}",
                        attachLog: true
                    )
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code...'
                // Integrate your code analysis tool here
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Use your security scanning tools here
            }
            post {
                always {
                    // Send an email notification with logs
                    emailext (
                        to: "${env.RECIPIENT_EMAIL}",
                        subject: "Jenkins Notification: Security Scan Stage Completed",
                        body: "The security scan stage has ${currentBuild.currentResult}: Check console output at ${env.BUILD_URL}",
                        attachLog: true
                    )
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                // Deploy your application to a staging environment
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Run integration tests on your staging environment
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                // Deploy your application to production
            }
        }
    }
    
    post {
        always {
            // Archive the logs for each build
            archiveArtifacts artifacts: '**/target/*.log', fingerprint: true
        }
    }
}
