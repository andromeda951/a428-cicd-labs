node {
    def dockerImage = 'node:16-buster-slim'

    stage('Build') {
        docker.image(dockerImage).inside("-p 3000:3000") {
            sh 'npm install'
        }
    }

    stage('Test') {
        docker.image(dockerImage).inside("-p 3000:3000") {
            sh './jenkins/scripts/test.sh'
        }
    }

    stage('Manual Approval') { 
        input message: 'Lanjutkan ke tahap Deploy?' 
        // sh './jenkins/scripts/kill.sh' 
    }

    stage('Deploy') { 
        docker.image(dockerImage).inside("-p 3000:3000") {
            sh './jenkins/scripts/deliver.sh' 
            sh 'sleep 1'
        }
    }
}
