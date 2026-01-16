node {
    checkout scm
    
    // Gunakan Docker socket dari jenkins-docker container
    docker.image('node:lts-buster-slim').withRun(
        '-p 3000:3000 -v ${WORKSPACE}:/app -w /app --network jenkins',
        'tail -f /dev/null'
    ) { c ->
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
