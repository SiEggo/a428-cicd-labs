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
                script {
                    def userInput = input(
                        id: 'userInput', 
                        message: 'Lanjutkan ke tahap Deploy?', 
                        parameters: [choice(choices: ['Proceed', 'Abort'], description: 'Pilih salah satu opsi', name: 'Pilihan')]
                    )
                    if (userInput == 'Abort') {
                        error('Pipeline dihentikan oleh pengguna.')
                    }
                }
            }
        }
        stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh'
                timeout(time: 1, unit: 'MINUTES') {
                    input message: 'Apakah Anda yakin ingin melanjutkan ke tahap kill.sh? (Klik "Proceed" untuk melanjutkan)'
                }
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}