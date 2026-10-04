pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Build') {
            steps {
                echo "Commit under test: ${env.GIT_COMMIT}"
                echo 'Task: Compile the source code and package it into a deployable artefact (JAR).'
                echo 'Tool: Apache Maven (mvn clean package)'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Task: Run unit tests to check each component works, then integration tests to check components work together.'
                echo 'Tools: JUnit 5 (unit), Mockito (mocking), Testcontainers (integration)'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Task: Analyse code for bugs, code smells, duplication and coverage against industry standards.'
                echo 'Tool: SonarQube (SonarScanner for Jenkins) with a quality gate'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Task: Scan code and dependencies for known vulnerabilities (CVEs).'
                echo 'Tools: OWASP Dependency-Check and Snyk'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Task: Deploy the application to the staging server (AWS EC2 staging instance).'
                echo 'Tool: AWS CodeDeploy (alternative: Ansible)'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Task: Run API and end-to-end tests on staging to confirm it works in a production-like environment.'
                echo 'Tools: Postman/Newman (API) and Selenium WebDriver (UI)'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Task: Release the verified build to the production server (AWS EC2 production instance).'
                echo 'Tool: AWS CodeDeploy using blue/green deployment'
            }
        }
    }

    post {
        success { echo 'Pipeline completed successfully.' }
        failure { echo 'Pipeline failed - check the stage logs above.' }
    }
}
