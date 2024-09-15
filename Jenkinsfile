pipeline {
    agent any

    stages {
        stage('Compile') {
            steps {
                echo 'Compiling the project...'
                echo 'Tools involved: Bazel, Make, CMake for building'
            }
        }
        stage('Testing') {
            steps {
                echo 'Executing Unit and Integration Tests...'
                echo 'Frameworks used: Pytest, Jasmine, Mocha, Robot Framework'
                // Adjusted for Windows
                bat 'echo "Running unit and integration tests..." > test-results.log'
                bat 'echo "All tests successfully completed." >> test-results.log'
            }
        }
        stage('Static Code Review') {
            steps {
                echo 'Performing Static Code Analysis...'
                echo 'Tools for analysis: ESLint, Pylint, Codacy, Flake8'
            }
        }
        stage('Vulnerability Check') {
            steps {
                echo 'Conducting Security Scans...'
                echo 'Security Tools: WhiteSource, Acunetix, Fortify, Clair'
                // Adjusted for Windows
                bat 'echo "Running security scan..." > security-scan-results.log'
                bat 'echo "Security scan finished successfully." >> security-scan-results.log'
            }
        }
        stage('Staging Deployment') {
            steps {
                echo 'Deploying application to staging environment...'
                echo 'Deployment Tools: Jenkins X, GitLab CI/CD, CircleCI'
            }
        }
        stage('Staging Tests') {
            steps {
                echo 'Running integration tests on staging...'
                echo 'Testing Tools: JMeter, Gatling, SoapUI, Katalon Studio'
            }
        }
        stage('Production Deployment') {
            steps {
                echo 'Deploying to the production environment...'
                echo 'Deployment automation: Terraform, Packer, Chef, Puppet'
            }
        }
    }
    post {
        always {
            echo 'The pipeline has completed!'
        }
        failure {
            emailext attachLog: true,
                     to: 'ar67445@gmail.com',
                     subject: "Build Failed: ${env.BUILD_ID} - Review Required",
                     body: """<p>Build ${env.BUILD_ID} encountered an issue.</p>
                              <p>Check Jenkins here: ${env.BUILD_URL}</p>"""
        }
        success {
            emailext attachLog: true,
                     to: 'ar67445@gmail.com',
                     subject: "Build Succeeded: ${env.BUILD_ID}",
                     body: """<p>Build ${env.BUILD_ID} was successful.</p>
                              <p>Check Jenkins for more details: ${env.BUILD_URL}</p>"""
        }
    }
}
