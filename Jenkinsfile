pipeline{
    agent any
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
                    attachments: '*.log'
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
                    attachments: '*.log'
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
