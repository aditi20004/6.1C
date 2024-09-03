pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    environment {
        STAGING_SERVER = 'staging.example.com'
        PRODUCTION_SERVER = 'production.example.com'
        RECIPIENT_EMAIL = 'shrivastavaditi14@gmail.com'
    }
    stages {
        stage('Check Workspace') {
            steps {
                // This step checks the current working directory
                bat 'echo %CD%'
            }
        }
        stage('Build') {
            steps {
                // Update this directory path to where your 'pom.xml' is located within your repo if it's not in the root
                // If your 'pom.xml' is in the root, you can remove the 'dir' block and run Maven directly
                dir('PathToYourProjectIfNotInRoot') {
                    echo 'Building the project...'
                    bat 'mvn clean install'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests...'
                // Make sure to adjust the directory if your tests also require being in a specific folder
                bat 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code...'
                // Include your code analysis tools commands here
                bat 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Security tools should be properly configured and command included here
                echo 'Placeholder for security scan command'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server...'
                // Include your staging deployment scripts or commands here
                echo 'Placeholder for deploy to staging command'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Adjust the directory if necessary and include the proper Maven command
                bat 'mvn verify -Denvironment=staging'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server...'
                // Include your production deployment scripts or commands here
                echo 'Placeholder for deploy to production command'
            }
        }
    }
    post {
        always {
            emailext (
                subject: "Jenkins Pipeline Status: ${currentBuild.fullDisplayName}",
                body: """<p>The Jenkins Pipeline ${currentBuild.fullDisplayName} has completed.</p>
                         <p>Status: ${currentBuild.currentResult}</p>
                         <p>Check the build details at: <a href='${BUILD_URL}'>${BUILD_URL}</a></p>""",
                to: "${RECIPIENT_EMAIL}"
            )
        }
    }
}
