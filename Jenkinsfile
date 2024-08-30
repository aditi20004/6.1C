pipeline {
agent any
stages {
stage('Build') {
    steps {
        // Example: Use Maven to build the project
        script {
            echo 'Building the project...'
            // sh 'mvn clean install' // Uncomment if using Maven
        }
    }
}
stage('Unit and Integration Tests') {
    steps {
        // Example: Run tests
        script {
            echo 'Running unit and integration tests...'
            // sh 'mvn test' // Uncomment if using Maven
        }
    }
}
stage('Code Analysis') {
    steps {
        // Example: Perform code analysis
        script {
            echo 'Performing code analysis...'
            // sh 'sonar-scanner' // Uncomment if using SonarQube
        }
    }
}
stage('Security Scan') {
    steps {
        // Example: Perform security scan
        script {
            echo 'Performing security scan...'
            // sh 'dependency-check.sh' // Uncomment if using OWASP Dependency-Check
        }
    }
}
stage('Deploy to Staging') {
    steps {
        script {
            echo 'Deploying to staging server...'
            // sh 'deploy_to_staging.sh' // Add your deployment script here
        }
    }
}
stage('Integration Tests on Staging') {
    steps {
        script {
            echo 'Running integration tests on staging...'
            // sh 'run_staging_tests.sh' // Add your integration test script here
        }
    }
}
stage('Deploy to Production') {
    steps {
        script {
            echo 'Deploying to production...'
            // sh 'deploy_to_production.sh' // Add your production deployment script here
        }
    }
}
}
post {
always {
    emailext(
     subject: 'Build Status: ${BUILD_STATUS}',
body: '''<p>Build ${BUILD_STATUS}: Check console output at <a href="${BUILD_URL}">here</a></p>''',
recipientProviders: [[$class: 'DevelopersRecipientProvider']],
to: 'aditi.shrivastav911@gmail.com'
)

    )
}
}
}
