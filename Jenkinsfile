pipeline {
    agent any
    environment {
        DIRECTORY_PATH = "/path/to/code"
        PRODUCTION_ENVIRONMENT = "AWS EC2"
        BUILD_AUTOMATION = "Jenkins"
        UNIT_TEST = "NUnit"
        INTEGRATION_TEST = "Testsigma"
        CODE_ANALYSIS = "FindBugs"
        SECURITY_SCAN = "SonarQube"
        STAGING_SERVER = "AWS EC2"
    }
    stages {
        stage('Build') {
            steps {
                echo "Build the source code using ${env.BUILD_AUTOMATION}"
                echo "Compiling and packaging the code."
            }
        }
        
        stage('Test') {
            steps {
                echo "Running Unit Tests using ${env.UNIT_TEST}"
                sleep 5
                echo "Running Integration Tests using ${env.INTEGRATION_TEST}"
                sleep 5
                echo "Unit and Integration Test completed!"
            }
            post{
                failure {
                    emailext subject: 'TESTING STATUS - FAILURE: ${currentBuild.fullDisplayName}',
                    to: 'haile1994@gmail.com',
                    body: 'Check log attachment below',
                    attachLog: true
                }
                success {
                    emailext subject: "TESTING STATUS - SUCCESS: ${currentBuild.fullDisplayName}",
                    to: 'haile1994@gmail.com',
                    body: "The pipeline testing status is ${buildStatus}",
                    attachLog: true
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo "Check the quality of the code using ${env.CODE_ANALYSIS}"
                sleep 5
                echo "Code Analysis completed!"
            }
        }
        
        stage('Security Scan') {
            steps {
                echo "Performing security scan on the code using ${env.SECURITY_SCAN}"
                sleep 5
                echo "Security Scan completed!"
            }
            post{
                failure {
                    mail to: "haile1994@gmail.com",
                    subject: "SECURITY SCAN - FAILURE: ${currentBuild.fullDisplayName}",
                    body: "Security scan failed!"
                }
                success {
                    mail to: "haile1994@gmail.com",
                    subject: "SECURITY SCAN - SUCCESS: ${currentBuild.fullDisplayName}",
                    body: "Security scan was successful!"
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to ${env.STAGING_SERVER}"
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on the staging environment."
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo "Deploy the application to ${env.PRODUCTION_ENVIRONMENT}"
            }
        }
    }
}
