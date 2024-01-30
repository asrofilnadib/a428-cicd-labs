node {
    docker.image('node:lts-buster-slim').withRun('-p 3000:3000') {
        stage('Build') {
            script {
                sh 'npm install'
            }
        }
        stage('Test') {
            script {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            script {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the website? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
