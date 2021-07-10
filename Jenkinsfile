pipeline {
    agent any 
    stages {
        stage('Build') {
            steps {
                echo 'Building DBHub.io daemons'
                sh 'cd docker && docker build --label dbhub .'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing daemons'
            }
        }
    }
}
