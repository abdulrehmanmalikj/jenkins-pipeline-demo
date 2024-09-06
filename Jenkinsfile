pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished!'
        }
        failure {
            mail to: 'ar67445@gmail.com',
                 subject: "Jenkins Build Failed: ${env.BUILD_ID}",
                 body: "Build ${env.BUILD_ID} failed. Check Jenkins for details."
        }
        success {
            mail to: 'ar67445@gmail.com',
                 subject: "Jenkins Build Success: ${env.BUILD_ID}",
                 body: "Build ${env.BUILD_ID} completed successfully."
        }
    }
}
