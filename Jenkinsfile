pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') { 
            steps {
                sh './jenkins/scripts/test.sh' 
            }
        }
        stage('Manual Approval') {
            steps {
                
                input message: 'Lanjutkan ke tahap Deploy?', submitter: 'user'
            }
        }
        stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                echo 'Menunggu 1 menit sebelum mengakhiri aplikasi...'
                sleep 60
                echo 'Waktu menunggu telah selesai. Melanjutkan ke langkah berikutnya.'
            }
        }
    }
}