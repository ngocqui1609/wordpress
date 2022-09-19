pipeline {
    agent any

    stages {
        def jobName = currentBuild.fullDisplayName
        def mailToRecipients = 'huynhthan45678@gmail.com'
        def useremail='huynhthan45678@gmail.com'
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
//         stage('Approval') {
//             // no agent, so executors are not used up when waiting for approvals
//             //agent none
//             steps {
//                 script {
//                     def deploymentDelay = input id: 'Deploy', message: 'Deploy to production?', submitter: 'qui'
//                 }
//             }
//         }
        stage('Deploy') {
            def userAborted = false
            emailext body: '''
            Please go to console output of ${BUILD_URL}input to approve or Reject.<br>''',
            mimeType: 'text/html',
            subject: "[Jenkins] ${jobName} Build Approval Request",
            from: "${useremail}",
            to: "${mailToRecipients}",
            recipientProviders: [[$class: 'CulpritsRecipientProvider']]
            try {
                userInput = input submitter: 'vagrant', message: 'Do you approve?'
            } catch (org.jenkinsci.plugins.workflow.steps.FlowInterruptedException e) {
              cause = e.causes.get(0)
              echo "Aborted by " + cause.getUser().toString()
                    userAborted = true
                echo " SYSTEM aborted, but looks like timeout period didn't complete. Aborting."
            }
            if (userAborted) {
                currentBuild.result = 'ABORTED'
            } else {
                echo 'Deploying....'
            }
        }
//         stage('Approval') {
//             // no agent, so executors are not used up when waiting for approvals
//             //agent none
//             steps {
//                 script {
//                     def deploymentDelay = input id: 'Deploy', message: 'Deploy to production?', submitter: 'rkivisto,admin', parameters: [choice(choices: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24'], description: 'Hours to delay deployment?', name: 'deploymentDelay')]
//                     sleep time: deploymentDelay.toInteger(), unit: 'HOURS'
//                 }
//             }
//         }
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
