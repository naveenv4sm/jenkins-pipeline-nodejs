pipeline {
    agent any

    tools {
        nodejs 'NodeJS'
    }

    environment {
        GIT_CREDENTIALS_ID = '12fcc0bf-c799-455c-9db1-a14e7087fdc0' 
        REPO_URL = 'https://github.com/naveenv4sm/jenkins-pipeline-nodejs.git'
        BRANCH = 'main'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    git branch: BRANCH, credentialsId: GIT_CREDENTIALS_ID, url: REPO_URL
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    sh 'node --version'
                    sh 'npm install'
                    sh 'npm install gulp-cli' // Install locally to avoid permission issues
                    sh 'npx gulp lint' // Use npx to execute
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh 'node --version'
                    sh 'npx gulp test'
                }
            }
        }

        stage('NPM Build') {
            steps {
                script {
                    sh 'npm run build'
                }
            }
        }
    }

    post {
        always {
            echo 'One way or another, I have finished'
            deleteDir() // Clean up workspace
        }
        success {
            echo 'I succeeded!'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
            echo 'I failed :('
        }
        changed {
            echo 'Things were different before...'
        }
    }
}
