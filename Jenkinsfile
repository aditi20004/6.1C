pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the project...'
                    // For Windows, you might use a batch command instead of `sh`
                    bat 'mvn clean install' // Use `bat` instead of `sh` for Windows
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests...'
                    bat 'mvn test' // Use `bat` instead of `sh` for Windows
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    echo 'Performing code analysis...'
                    // Assuming SonarQube is installed, otherwise adjust the command
                    bat 'sonar-scanner' // Use `bat` instead of `sh` for Windows
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan...'
                    // Assuming Dependency-Check is installed, otherwise adjust the command
                    bat 'dependency-check.bat' // Use `bat` instead of `sh` for Windows
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to staging server...'
                    // Replace this with your Windows-specific deployment command
                    bat 'deploy_to_staging.bat' // Example: Windows batch script
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging...'
                    // Replace this with your Windows-specific test script
                    bat 'run_staging_tests.bat' // Example: Windows batch script
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production...'
                    // Replace this with your Windows-specific deployment command
                    bat 'deploy_to_production.bat' // Example: Windows batch script
                }
            }
        }
    }
    post {
        always {
            emailext (
                subject: "Jenkins Build: ${currentBuild.fullDisplayName}",
                body: """<p>Build status: ${currentBuild.currentResult}</p>
                         <p>Please check the attached log for more details.</p>""",
                to: 'aditi.shrivastav911@gmail.com',
                attachLog: true,
                compressLog: true,
                mimeType: 'text/html'
            )
        }
    }
}
