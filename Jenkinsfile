node {
    docker.image('node:18-buster-slim').withRun('-p 3000:3000') { container ->
        
        
        stage('Build') {
            sh 'npm install'
        }
         
       
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
    }
}