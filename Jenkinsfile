pipeline {
    agent any

    environment {
        GIT_URL = 'https://github.com/adsz/jenkins-slack' // Define GIT_URL if needed globally
    }

    stages {
        stage('Set Env Variables') {
            steps {
                script {
                    // Retrieve commit ID and branch name, set them as environment variables
                    env.GIT_COMMIT_ID = sh(script: 'git rev-parse HEAD', returnStdout: true).trim()            
                    env.BRANCH_NAME = sh(script: "git rev-parse --abbrev-ref HEAD", returnStdout: true).trim()

                    // Retrieve the full commit ID, trim it, and get the last 6 characters using substring method
                    def fullCommitId = env.GIT_COMMIT_ID // Reuse the retrieved commit ID
                    env.GIT_COMMIT_ID = fullCommitId.length() > 6 ? fullCommitId[-6..-1] : fullCommitId
                }
            }
        }
        stage('Get commit details') {
            steps {
                script {
                    // Retrieve the commit message and author using the correct commit ID
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
