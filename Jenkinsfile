pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the project...'
                    sh 'mvn clean install' // Uncomment if using Maven
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests...'
                    sh 'mvn test' // Uncomment if using Maven
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    echo 'Performing code analysis...'
                    sh 'sonar-scanner' // Uncomment if using SonarQube
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan...'
                    sh 'dependency-check.sh' // Uncomment if using OWASP Dependency-Check
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to staging server...'
                    sh 'deploy_to_staging.sh' // Add your deployment script here
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging...'
                    sh 'run_staging_tests.sh' // Add your integration test script here
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production...'
                    sh 'deploy_to_production.sh' // Add your production deployment script here
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
                compressLog: true,  // Compresses log before attaching
                mimeType: 'text/html'  // Email format set to HTML
            )
        }
    }
}
