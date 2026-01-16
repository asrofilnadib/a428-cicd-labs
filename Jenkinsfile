node {
    checkout scm
    
    def reactContainer
    docker.image('node:lts-buster-slim').withRun('-p 3000:3000') { c ->
        reactContainer = c
        
        stage('Build') {
            sh "docker exec ${c.id} npm install"
        }
        stage('Test') {
            sh "docker exec ${c.id} ./jenkins/scripts/test.sh"
        }
        stage('Deliver') {
            sh "docker exec ${c.id} ./jenkins/scripts/deliver.sh"
            input message: 'Finished using the website? (Click "Proceed" to continue)'
            sh "docker exec ${c.id} ./jenkins/scripts/kill.sh"
        }
    }
}
