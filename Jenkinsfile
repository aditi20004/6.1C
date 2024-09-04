pipeline{
    agent any
    stages{
        stage("Build"){
            steps{
                echo "Maven Was used to automate the build process, plus it compiled and pakaged the code"
            }
            post{
                success{
                    mail to: "shrivastavaditi14@gmail.com",
                    subject: "Jenkins Build report",
                    body: "the build with maven was successfull"
                }
                failure{
                    mail to: "shrivastavaditi14@gmail.com",
                    subject: "Jenkins Build report",
                    body: "Unfortunately the Build couldnt be compeleted successfully"
                }
            }
        }
        stage("Unit and Integration Tests"){
            steps{
                echo "JUnit and selenium were used to perform unit and integration tests To ensure code runs as expected And all the components of application come together as expected"
            }
            post{
                success{
                    mail to: "shrivastavaditi14@gmail.com",
                    subject: "Unit and Integration Tests report",
                    body: "Unit and Integration Tests went well and this stage of devvelopment is clear"
                }
                failure{
                    mail to: "shrivastavaditi14@gmail.com",
                    subject: "Unit and Integration Tests report",
                    body: "Unfortunately the Unit and Integration Tests couldnt be compeleted successfully"
                }
            }
        }
        stage("Code Analysis"){
            steps{
                echo "Sonar Qube was used to analyse code to make sure it meets industry standards"
            }
        }
        stage("Security Scan"){
            steps{
                echo "OWASP ZAP is used To scan the code and identify the vulnerabilities and perform a security scan"
            }
            post{
                success{
                    mail to: "shrivastavaditi14@gmail.com",
                    subject: "Security Scan report",
                    body: "Great News! Security Scan was successfull "
                }
                failure{
                    mail to: "shrivastavaditi14@gmail.com",
                    subject: "Security Scan report",
                    body: "Unfortunately! the Security Scan report couldnt be compeleted successfully"
                }
            }
        }
        stage("Deploy to Staging"){
            steps{
                echo "Jenkins to deploy to staging"
            }
        }
        stage(" Integration Tests on Staging"){
            steps{
                echo "Apache JMeter is used to run integration tests on the staging environment to ensure the application functions as expected in a production-lik environment."
            }
            post{
                success{
                    mail to: "shrivastavaditi14@gmail.com",
                    subject: "Integration Tests on Staging report",
                    body: "Integration Tests on Staging was successfull"
                }
                failure{
                    mail to: "shrivastavaditi14@gmail.com",
                    subject: "Integration Tests on Staging report",
                    body: "Unfortunate the Integration Test on Staging report couldnt be compeleted successfully"
                }
            }
        }
        stage("Deploy to Production"){
            steps{
                echo "Using Jenkins to deploy to production server"
            }
        }

    }
}
