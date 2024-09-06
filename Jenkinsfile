pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                // You can use Maven or Gradle
                // Example: sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Example tool: JUnit, TestNG
                // Example: sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'
                // Example tool: SonarQube
                // Example: sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                // Example tool: OWASP Dependency-Check
                // Example: sh 'dependency-check --project JenkinsPipeline --scan ./'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // Example: Deploy to AWS EC2 using SSH or AWS CLI
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Example: run integration tests using a test suite
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                // Example: Deploy to AWS EC2 using SSH or AWS CLI
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