pipeline {
    agent any
    triggers {
        pollSCM('H/5 * * * *')
    }
    environment {
        EMAIL = 's226112421@deakin.edu.au'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Task: Compile and package the code'
                echo 'Tool: Maven'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Task: Run unit tests and integration tests'
                echo 'Tool: JUnit (unit), Selenium (integration)'
            }
            post {
                always {
                    emailext(
                        to: "${EMAIL}",
                        subject: "Unit and Integration Tests: ${currentBuild.currentResult}",
                        body: "The Unit and Integration Tests stage finished with status: ${currentBuild.currentResult}. Log attached.",
                        attachLog: true
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Task: Analyse code quality against industry standards'
                echo 'Tool: SonarQube'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Task: Scan code for security vulnerabilities'
                echo 'Tool: OWASP Dependency-Check'
            }
            post {
                always {
                    emailext(
                        to: "${EMAIL}",
                        subject: "Security Scan: ${currentBuild.currentResult}",
                        body: "The Security Scan stage finished with status: ${currentBuild.currentResult}. Log attached.",
                        attachLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Task: Deploy application to staging server'
                echo 'Tool: AWS EC2 instance (via AWS CLI)'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Task: Run integration tests in the staging environment'
                echo 'Tool: Selenium / Postman'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Task: Deploy application to production server'
                echo 'Tool: AWS EC2 instance (via AWS CLI)'
            }
        }
    }
}
