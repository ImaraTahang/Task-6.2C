pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                echo "Building code.."
                //maven can be used for build automation
            }
        }
        stage('Tests'){
            steps{
                echo "Running unit and integration tests.."
                //maven can also be used to run these tests
            }
            post {
                always {
                    emailext to: "Imaratahang@gmail.com",
                    subject: "Test Status Email", 
                    body: "Tests were successful",
                    //attachLog: true
                }
            }
        }
        stage('Code Analysis'){
            steps{
                echo "Analysing code.."
                // use Checkstyle, FindBugs or PMD
            }
        }
        stage('Security Scan'){
            steps {
                echo "Performing security scan.."
                // use Probely Security Scanner Plugin
            }
            post {
                always {
                    emailext to: "Imaratahang@gmail.com",
                    subject: "Security Scan Status Email", 
                    body: "Security Scan was successful",
                    //attachLog: true
                }
            }
        }
        stage('Deploy to Staging'){
            steps{
                echo "Deploying to staging server.."
                // use AWS EC2
            }
        }
        stage('Integration Tests on Staging'){
            steps{
               echo "Running integration tests.."
                // use JUnit
            }
        }
        stage('Deploy to Production'){
            steps{
                echo "Deploying to production server.."
                // use AWS EC2
            }
        }
    }
}

