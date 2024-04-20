pipeline {
    agent any
    
    environment {
        DIRECTORY_PATH = "/path/to/code"
        TESTING_ENVIRONMENT = "testing-environment"
        PRODUCTION_ENVIRONMENT = "production-environment"
    }
    stages {
        stage('Build') {
            steps {
                echo "Fetch the source code from the directory path ${env.DIRECTORY_PATH}"
                echo "Compile the code and generate any necessary artifacts."
                bat "java -version"
                bat "java -jar jenkins.war"
            }
            post{
                success{
                    mail to: "haile1994@gmail.com",
                    subject: "Build Status Email",
                    body: "Build was successful!"
                }
            }
        }
        
        stage('Test') {
            steps {
                echo "Unit tests"
                echo "Integration tests"
            }
        }
        
        stage('Code Quality Check') {
            steps {
                echo "Check the quality of the code"
            }
        }
        
        stage('Approval') {
            steps {
                sleep 10
            }
        }
        
        stage('Deploy') {
            steps {
                echo "Deploy the application to ${env.TESTING_ENVIRONMENT}"
            }
        }
        
        stage('Deploy to Production') {
            steps {
           //     retry(2){
           //         echo "Deploy the code to ${env.PRODUCTION_ENVIRONMENT}"
             //   }
              //  timeout(time: 3, unit: 'SECONDS')
               // {
                //    sleep 5
               // }
                echo "Deploy the code to ${env.PRODUCTION_ENVIRONMENT}"
            }
            post{
                failure {
                    mail to: "haile1994@gmail.com",
                    subject: "FAILURE: ${currentBuild.fullDisplayName}",
                    body: "Deploy to production was fail!"
                }
                success {
                    mail to: "haile1994@gmail.com",
                    subject: "SUCCESS: ${currentBuild.fullDisplayName}",
                    body: "Deploy to production was successful!"
                }
            }
        }
    }
}
