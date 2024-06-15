pipeline {
    agent any

    stages {
        stage('Set Env Variables') {
            steps {
                script {
                    // Set the full commit ID
                    env.GIT_COMMIT_ID = sh(script: 'git rev-parse HEAD', returnStdout: true).trim()
                    // Try to get the branch name, fallback to 'main' if in detached HEAD state
                    env.BRANCH_NAME = sh(script: "git rev-parse --abbrev-ref HEAD", returnStdout: true).trim()
                    if (env.BRANCH_NAME == 'HEAD') {
                        env.BRANCH_NAME = 'main'  // Assumes 'main' is the default branch if HEAD is detached
                    }
                }
            }
        }
        stage('Get commit details') {
            steps {
                script {
                    // Retrieve the commit message and author using the full commit ID
                    env.GIT_COMMIT_MSG = sh(script: "git log -1 --pretty=%B ${env.GIT_COMMIT_ID}", returnStdout: true).trim()
                    env.GIT_AUTHOR = sh(script: "git log -1 --pretty=%cn ${env.GIT_COMMIT_ID}", returnStdout: true).trim()
                }
            }
        }
        stage('Slack') {
            steps {
                // Send the Slack notification with all the details
                slackSend color: 'good', message: "${env.GIT_AUTHOR}: ${env.GIT_COMMIT_MSG} ${env.BRANCH_NAME} ${env.GIT_COMMIT_ID} ${env.GIT_URL}"
                slackSend color: 'good', message: "${env.JOB_NAME} - #${env.BUILD_NUMBER}: Polska Gurom!"
            }
        }
    }
}
