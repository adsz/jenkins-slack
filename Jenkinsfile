pipeline {
  agent any
  stages {
    stage('Slack') {
      steps {
        slackSend color: 'good', message: "${env.JOB_NAME} - #${env.BUILD_NUMBER}: Ale jaja panie Czaja!"
      }
      steps {
        slackSend color: 'good', message: "${env.JOB_NAME} - #${env.BUILD_NUMBER}: Ale jaja panie Czaja!"
      }
    }
  }
}
