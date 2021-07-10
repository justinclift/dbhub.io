pipeline {
    agent any 
    stages {
        stage('Build') {
            steps {
                echo 'Building DBHub.io daemons'
                sh 'docker build . --label dbhubtest -f docker/Dockerfile'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing daemons'
                echo 'TBD...'
            }
        }
    }
}
