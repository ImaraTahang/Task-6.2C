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
                sh 'mvn clean package'
            }
        }
        stage('Tests'){
            steps{
                echo "Running unit and integration tests"
                sh 'mvn test'
            }
            post {
                success {
                    mail to: "Imaratahang@gmail.com",
                    subject: "Test Status Email", 
                    body: "Tests were successful",
                    attachmentsPattern: "*.log"
                }
            }
        }
        stage('Code Analysis'){
            steps{
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Security Scan'){
            steps {
                withEnv(['ZAP_PORT=8090']) {
                    sh 'zap.sh -daemon -port ${ZAP_PORT} -config api.disablekey=true'
                    sh 'mvn verify -Psecurity'
                }
            }
            post {
                success {
                    mail to: "Imaratahang@gmail.com",
                    subject: "Security Scan Status Email", 
                    body: "Security scan was successful",
                    attachmentsPattern: "*.log"
                }
            }
        }
        stage('Deploy to Staging'){
            steps{
                sshagent(['my-ssh-key']) {
                    sh 'ssh -o StrictHostKeyChecking=no user@staging-server "cd /path/to/app && ./deploy.sh"'
                }
            }
        }
        stage('Integration Tests on Staging'){
            steps{
                sh 'mvn verify -Pintegration-tests-staging'
            }
        }
        stage('Deploy to Production'){
            steps{
                sshagent(['my-ssh-key']) {
                    sh 'ssh -o StrictHostKeyChecking=no user@production-server "cd /path/to/app && ./deploy.sh"'
                }
            }
        }
    }
}
