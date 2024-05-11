pipeline {
    agent any

    stages {
        stage('Set Env Variables') {
            steps {
                script {
                    // Retrieve and set the full commit ID and branch name as environment variables
                    env.GIT_COMMIT_ID = sh(script: 'git rev-parse HEAD', returnStdout: true).trim()            
                    env.BRANCH_NAME = sh(script: "git rev-parse --abbrev-ref HEAD", returnStdout: true).trim()
                }
            }
        }
        stage('Get commit details') {
            steps {
                script {
                    // Use the full commit ID to retrieve the commit message and author
                    env.GIT_COMMIT_MSG = sh(script: "git log -1 --pretty=%B ${env.GIT_COMMIT_ID}", returnStdout: true).trim()
                    env.GIT_AUTHOR = sh(script: "git log -1 --pretty=%cn ${env.GIT_COMMIT_ID}", returnStdout: true).trim()
                }
            }
        }
        stage('Slack') {
            steps {
                // Send messages to Slack with retrieved details
                slackSend color: 'good', message: "${env.GIT_AUTHOR}: ${env.GIT_COMMIT_MSG} ${env.BRANCH_NAME} ${env.GIT_COMMIT_ID} ${env.GIT_URL}"
                slackSend color: 'good', message: "${env.JOB_NAME} - #${env.BUILD_NUMBER}: Ale jaja panie Czaja!"
            }
        }
    }
}
