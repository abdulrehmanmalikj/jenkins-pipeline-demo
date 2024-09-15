pipeline {
    
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build'
                echo 'Task: Build the code using a build automation tool'
                echo 'Tools: Bazel, Make, CMake'
            }
            post {
                failure {
                    script {
                        emailext (
                            to: 'ar67445@gmail.com',
                            subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Build Stage",
                            body: "Build failed. Please check the logs for details.",
                            attachLog: true
                        )
                    }
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Unit and Integration Tests'
                echo 'Task: Run unit tests and integration tests'
                echo 'Tools: Pytest, Jasmine, Mocha, Robot Framework'
                sh 'echo "Running unit tests..." > unit-tests.log'
                // Add actual test commands here, e.g., sh 'npm test'
                sh 'echo "Tests completed successfully." >> unit-tests.log'
            }
            post {
                always {
                    script {
                        def buildStatus = currentBuild.result ?: 'SUCCESS'
                        def subject = "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} - Unit and Integration Tests ${buildStatus}"
                        def body = """
                        Unit and Integration Tests Status: ${buildStatus}
                        Job: ${env.JOB_NAME}
                        Build Number: ${env.BUILD_NUMBER}
                        """
                        emailext (
                            to: 'ar67445@gmail.com',
                            subject: subject,
                            body: body,
                            attachmentsPattern: 'unit-tests.log'
                        )
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Analysis'
                echo 'Task: Analyze code quality and adherence to industry standards'
                echo 'Tools: ESLint, Pylint, Codacy, Flake8'
            }
            post {
                failure {
                    script {
                        emailext (
                            to: 'ar6744@gmail.com',
                            subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Code Analysis Stage",
                            body: "Code analysis failed. Please check the logs for details.",
                            attachLog: true
                        )
                    }
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan'
                echo 'Task: Scan the code for security vulnerabilities'
                echo 'Tools: WhiteSource, Acunetix, Fortify, Clair'
                sh 'echo "Running security scan..." > security-scan.log'
                sh 'echo "Security scan completed successfully." >> security-scan.log'
            }
            post {
                always {
                    script {
                        def buildStatus = currentBuild.result ?: 'SUCCESS'
                        def subject = "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} - Security Scan ${buildStatus}"
                        def body = """
                        Security Scan Status: ${buildStatus}
                        Job: ${env.JOB_NAME}
                        Build Number: ${env.BUILD_NUMBER}
                        """
                        emailext (
                            to: 'ar67445@gmail.com',
                            subject: subject,
                            body: body,
                            attachmentsPattern: 'security-scan.log'
                        )
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to Staging'
                echo 'Task: Deploy the application to a staging environment'
                echo 'Tools: Jenkins X, GitLab CI/CD, CircleCI'
            }
            post {
                failure {
                    script {
                        emailext (
                            to: 'ar67445@gmail.com',
                            subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Deploy to Staging Stage",
                            body: "Deployment to staging failed. Please check the logs for details.",
                            attachLog: true
                        )
                    }
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging'
                echo 'Task: Run integration tests in the staging environment'
                echo 'Tools: JMeter, Gatling, SoapUI, Katalon Studio'
            }
            post {
                failure {
                    script {
                        emailext (
                            to: 'ar67445@gmail.com',
                            subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Integration Tests Stage",
                            body: "Integration tests on staging failed. Please check the logs for details.",
                            attachLog: true
                        )
                    }
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production'
                echo 'Task: Deploy the application to the production server'
                echo 'Tools: Terraform, Packer, Chef, Puppet'
            }
            post {
                failure {
                    script {
                        emailext (
                            to: 'ar67445@gmail.com',
                            subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Deploy to Production Stage",
                            body: "Deployment to production failed. Please check the logs for details.",
                            attachLog: true
                        )
                    }
                }
            }
        }
    }
    post {
        always {
            script {
                def buildStatus = currentBuild.result ?: 'SUCCESS'
                def subject = "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} - ${buildStatus}"
                def body = """
                Build Status: ${buildStatus}
                Job: ${env.JOB_NAME}
                Build Number: ${env.BUILD_NUMBER}
                """
                emailext (
                    to: 'ar67445@gmail.com',
                    subject: subject,
                    body: body,
                    attachLog: true
                )
            }
        }
    }
}
