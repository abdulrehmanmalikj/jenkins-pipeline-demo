pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                echo 'Tools used: Maven for Java projects, npm for Node.js projects.'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                echo 'Tools used: JUnit for Java, NUnit for .NET, Mocha for Node.js.'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'
                echo 'Tools used: SonarQube for static code analysis.'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                echo 'Tools used: OWASP Dependency-Check for dependency vulnerabilities.'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                echo 'Tools used: Docker for containerization, Kubernetes or Helm for orchestration.'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                echo 'Tools used: Selenium for UI testing, Postman for API testing.'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                echo 'Tools used: Jenkins deployment plugins, Docker, Kubernetes/Helm.'
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished!'
        }
        failure {
            emailext attachLog: true,
                     to: 'ar67445@gmail.com',
                     subject: "Jenkins Build Failed: ${env.BUILD_ID}",
                     body: """<p>Build ${env.BUILD_ID} failed.</p>
                              <p>Check Jenkins for details: ${env.BUILD_URL}</p>"""
        }
        success {
            emailext attachLog: true,
                     to: 'ar67445@gmail.com',
                     subject: "Jenkins Build Success: ${env.BUILD_ID}",
                     body: """<p>Build ${env.BUILD_ID} completed successfully.</p>
                              <p>Check Jenkins for details: ${env.BUILD_URL}</p>"""
        }
    }
}
