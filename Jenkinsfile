pipeline {

    agent none

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'npm install'
            }
        }
        stage('Dev01') {
            steps {
                echo 'Testing...'
                sh 'npm test'
            }
        }
    }
}
