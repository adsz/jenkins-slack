pipeline {
  agent any
  stages {
    stage('Slack') {
      steps {
        slackSend color: 'good', message: "${env.JOB_NAME} - #${env.BUILD_NUMBER}: Siemanko z Jenkinsa i GitHuba"
      }
    }
  }
}
