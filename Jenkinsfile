pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Use SSH to deploy to EC2 instance
                    sshagent(['03e8a610-263c-4f28-ac79-1ad1a7674d60']) {
                        sh 'ssh ec2-user@34.228.230.226 "git pull && mvn clean install && echo poop > test.txt"'
                    }
                }
            }
        }
    }
}
