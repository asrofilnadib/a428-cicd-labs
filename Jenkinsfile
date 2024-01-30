pipeline {
    agent {
        docker {
            image 'node:lts-buster-slim'
            args '-p 3000:3000'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh './jenkins/scripts/test.sh'
                }
            }
        }
        stage('Deliver') {
            steps {
                script {
                    sh './jenkins/scripts/deliver.sh'
                    input message: 'Finished using the website? (Click "Proceed" to continue)'
                    sh './jenkins/scripts/kill.sh'
                }
            }
        }
    }
}
