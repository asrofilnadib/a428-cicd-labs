node {
    // Definisikan kontainer Docker
    def nodejsImage = docker.image('node:16-buster-slim').run('-p 3000:3000')

    try {
        // Langkah Build
        stage('Build') {
            nodejsImage.inside {
                // Perintah yang dijalankan dalam kontainer Docker
                sh 'npm install'
            }
        }
    } finally {
        // Hentikan kontainer Docker setelah selesai
        nodejsImage.stop()
    }
}