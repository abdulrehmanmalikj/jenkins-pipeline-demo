pipeline {
    agent any

    // Define common variables and functions
    environment {
        RECIPIENT = 'ar67445@gmail.com'
    }

    // Function to send email notifications
    def sendEmail(String to, String subject, String body, String attachments = null) {
        emailext (
            to: to,
            subject: subject,
            body: body,
            attachmentsPattern: attachments ?: '',
            attachLog: attachments == null ? true : false
        )
    }

    stages {
        stage('Compile') {
            steps {
                echo 'Stage 1: Compile'
                echo 'Task: Compile the source code'
                echo 'Tools: GCC, Make, CMake'
                sh 'make compile > compile.log'
            }
            post {
                failure {
                    script {
                        sendEmail(
                            env.RECIPIENT,
                            "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Compile Stage",
                            "Compilation failed. Please check the compile.log for details.",
                            'compile.log'
                        )
                    }
                }
            }
        }

        stage('Static Code Analysis') {
            steps {
                echo 'Stage 2: Static Code Analysis'
                echo 'Task: Perform static analysis on the codebase'
                echo 'Tools: ESLint, PMD, FindBugs'
                sh 'eslint . --output-file eslint-report.json'
            }
            post {
                always {
                    script {
                        def buildStatus = currentBuild.result ?: 'SUCCESS'
                        sendEmail(
                            env.RECIPIENT,
                            "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} - Static Code Analysis ${buildStatus}",
                            """
                            Static Code Analysis Status: ${buildStatus}
                            Job: ${env.JOB_NAME}
                            Build Number: ${env.BUILD_NUMBER}
                            """,
                            'eslint-report.json'
                        )
                    }
                }
            }
        }

        stage('Dependency Management') {
            steps {
                echo 'Stage 3: Dependency Management'
                echo 'Task: Manage and update project dependencies'
                echo 'Tools: npm, Yarn, Bundler'
                sh 'yarn install --frozen-lockfile > dependency.log'
            }
            post {
                failure {
                    script {
                        sendEmail(
                            env.RECIPIENT,
                            "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Dependency Management Stage",
                            "Dependency management failed. Please check the dependency.log for details.",
                            'dependency.log'
                        )
                    }
                }
            }
        }

        stage('Dynamic Security Testing') {
            steps {
                echo 'Stage 4: Dynamic Security Testing'
                echo 'Task: Perform dynamic security assessments'
                echo 'Tools: Burp Suite, ZAP, AppScan'
                sh 'zap.sh -daemon -config api.disablekey=true -port 8080'
                sh 'echo "Dynamic security testing completed." > dynamic-security.log'
            }
            post {
                always {
                    script {
                        def buildStatus = currentBuild.result ?: 'SUCCESS'
                        sendEmail(
                            env.RECIPIENT,
                            "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} - Dynamic Security Testing ${buildStatus}",
                            """
                            Dynamic Security Testing Status: ${buildStatus}
                            Job: ${env.JOB_NAME}
                            Build Number: ${env.BUILD_NUMBER}
                            """,
                            'dynamic-security.log'
                        )
                    }
                }
            }
        }

        stage('Staging Deployment') {
            steps {
                echo 'Stage 5: Staging Deployment'
                echo 'Task: Deploy the application to the staging environment'
                echo 'Tools: Terraform, Helm, OpenShift'
                sh 'terraform apply -auto-approve > staging-deploy.log'
            }
            post {
                failure {
                    script {
                        sendEmail(
                            env.RECIPIENT,
                            "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Staging Deployment Stage",
                            "Deployment to staging failed. Please check the staging-deploy.log for details.",
                            'staging-deploy.log'
                        )
                    }
                }
            }
        }

        stage('Staging Validation') {
            steps {
                echo 'Stage 6: Staging Validation'
                echo 'Task: Validate the deployment in the staging environment'
                echo 'Tools: Postman, Newman, Gatling'
                sh 'newman run staging-collection.json > staging-validation.log'
            }
            post {
                failure {
                    script {
                        sendEmail(
                            env.RECIPIENT,
                            "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Staging Validation Stage",
                            "Staging validation failed. Please check the staging-validation.log for details.",
                            'staging-validation.log'
                        )
                    }
                }
            }
        }

        stage('Production Deployment') {
            steps {
                echo 'Stage 7: Production Deployment'
                echo 'Task: Deploy the application to the production environment'
                echo 'Tools: Jenkins X, Spinnaker, Flux'
                sh 'spinnaker deploy production > production-deploy.log'
            }
            post {
                failure {
                    script {
                        sendEmail(
                            env.RECIPIENT,
                            "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Production Deployment Stage",
                            "Deployment to production failed. Please check the production-deploy.log for details.",
                            'production-deploy.log'
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
                sendEmail(
                    env.RECIPIENT,
                    "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} - ${buildStatus}",
                    """
                    Build Status: ${buildStatus}
                    Job: ${env.JOB_NAME}
                    Build Number: ${env.BUILD_NUMBER}
                    """
                )
            }
        }
    }
}
