pipeline {
    agent any 
    stages {
        stage('Build') {
            steps {
                echo 'Building DBHub.io daemons'
                sh 'docker build --label dbhub docker'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing daemons'
            }
        }
    }
}
