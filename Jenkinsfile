pipeline{
    agent any
    tools { 
        maven 'Maven' 
        jdk 'JDK' 
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
                always {
                    emailext to: "Imaratahang@gmail.com",
                    subject: "Test Status Email", 
                    body: "Tests were successful",
                    attachLog: true
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
                withSonarQubeEnv('SonarQube Server') {
                    sh 'mvn sonar:sonar'
                }
            }
            post {
                always {
                    emailext to: "Imaratahang@gmail.com",
                    subject: "Security Scan Status Email", 
                    body: "Security Scan was successful",
                    attachLog: true
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

