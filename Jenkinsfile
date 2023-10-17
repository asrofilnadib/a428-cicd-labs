node {
    def customImage

    try {
        customImage = docker.image('node:16-buster-slim').withRun('-p 3000:3000')        
        customImage.inside {
            stage('Build') {
                sh 'npm install'
            }
            stage('Test') {
                sh './jenkins/scripts/test.sh'
            }
        }
    } finally {
        if (customImage) {
            customImage.stop()
        }
    }
}

