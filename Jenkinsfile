pipeline {
    agent any 
    stages {
        stage('Build') {
            steps {
                echo 'Building DBHub.io daemons'
                sh "docker build . --tag dbhubtest:${env.BUILD_ID} -f docker/Dockerfile"
            }
        }
        stage('Start daemons') {
            steps {
                echo 'Start daemons'
                sh "docker-compose -f tests/docker-compose.yml up -d"
            }
        }
        stage('Test daemons') {
            steps {
                echo 'Testing daemons'
                echo 'TBD...'
            }
        }
        stage('Shut down daemons') {
            steps {
                echo 'Shut down daemons'
                sh "docker-compose -f tests/docker-compose.yml down"
            }
        }
    }
}
