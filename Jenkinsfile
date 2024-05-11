pipeline {
  agent any
  stages {
    stage('Get commit details') {
        steps {
            script {
                env.GIT_COMMIT_MSG = sh (script: 'git log -1 --pretty=%B ${GIT_COMMIT}', returnStdout: true).trim()
                env.GIT_AUTHOR = sh (script: 'git log -1 --pretty=%cn ${GIT_COMMIT}', returnStdout: true).trim()
                env.GIT_COMMIT_ID = sh (script: 'git log -1 --pretty=%B ${GIT_COMMIT}', returnStdout: true).trim()
            }
    }
    }
    stage('Slack') {
      steps {
        slackSend color: 'good', message: "${env.GIT_AUTHOR}: ${env.GIT_COMMIT_MSG} ${env.BRANCH_NAME} ${env.GIT_COMMIT_ID} ${env.GIT_URL}"
        slackSend color: 'good', message: "${env.JOB_NAME} - #${env.BUILD_NUMBER}: Ale jaja panie Czaja!"
      }
    }
  }
}
