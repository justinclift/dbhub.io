pipeline {
    agent any 
    stages {
        stage('Build') {
            steps {
                echo 'Building DBHub.io daemons'
                sh 'docker build . --tag dbhubtest:${env.BUILD_ID} -f docker/Dockerfile'
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
