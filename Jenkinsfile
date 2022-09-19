pipeline {
    agent none
    stages {
        stage('Build') {
            agent any
            steps {
                echo 'compiling...'
            }
        }
        stage('Test') {
            agent any
            steps {
                echo 'testing...'
            }
        }
        stage('Approval') {
            // no agent, so executors are not used up when waiting for approvals
            agent none
            steps {
                script {
                    def deploymentDelay = input id: 'qui', message: 'Deploy to production?', submitter: 'qui'
//                     , parameters: [choice(choices: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24'], description: 'Hours to delay deployment?', name: 'deploymentDelay')]
//                     sleep time: deploymentDelay.toInteger(), unit: 'HOURS'
                }
            }
        }
        stage('Deploy') {
            agent any
            steps {
                    echo 'Deploying...'
            }
        }
    }
    
   post {
    success {
      echo "SUCCESSFUL"
    }
    failure {
      echo "FAILED"
    }
  }
}
