node {
    // Menentukan agent (agen Docker dengan gambar 'node:16-buster-slim')
    docker.image('node:16-buster-slim').withRun('-p 3000:3000') { container ->
        
        // Tahap 'Build'
        stage('Build') {
            // Langkah untuk memasang dependensi dengan npm
            sh 'npm install'
        }
        
        // Tahap 'Test'
        stage('Test') {
            // Menjalankan skrip uji dari file eksternal (test.sh)
            sh './jenkins/scripts/test.sh'
        }
    }
}