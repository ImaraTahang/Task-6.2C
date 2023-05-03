pipeline{
    agent any
    environment{
        DIRECTORY_PATH = "C:/Users/Imara/AppData/Local/Jenkins/.jenkins/jobs/Task 5.1P"
        TESTING_ENVIRONMENT = "Jenkins"
        PRODUCTION_ENVIRONMENT = "Imara"
    }
    stages{
        stage('Build'){
            steps{
                echo "fetch the source code from ${DIRECTORY_PATH}"
                echo "compile the code and generate any necessary artifacts"
            }
        }
        stage('Test'){
            steps{
                echo "Unit tests"
                echo "Integration tests"
            }
        }
        stage('Code Quality Check'){
            steps{
                echo "Check the quality of the code"
            }
        }
        stage('Deploy'){
            steps{
                echo "deploy the application to ${TESTING_ENVIRONMENT}"
            }
        }
        stage('Approval'){
            steps{
                sleep time: 10, unit: 'SECONDS'
            }
        }
        stage('Deploy to production'){
            steps{
                echo "fetch the source code from ${DIRECTORY_PATH}"
            }
        }
    }
}
