pipeline {
    agent any
    environment {
        EMAIL_RECIPIENT = 's222514502@deakin.edu.au'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build - Compiling and packaging the source code into an executable or deployable artifact using Maven.'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Unit and Integration Tests - Running automated tests with JUnit for unit testing and TestNG for integration testing.'
            }
            post {
                always {
                    saveLogsAndEmail('Unit and Integration Tests')
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Analysis - Performing automated code analysis with SonarQube to ensure code quality and adherence to coding standards.'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan - Identifying security vulnerabilities with OWASP ZAP for dynamic application security testing.'
            }
            post {
                always {
                    saveLogsAndEmail('Security Scan')
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to Staging - Deploying the built and tested application to a staging environment using Jenkins Deployment plugins or AWS CodeDeploy.'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging - Conducting additional integration tests in the staging environment using Selenium for web application testing.'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production - Deploying the application to the production server using Jenkins or AWS CodeDeploy.'
            }
        }
    }
}

def saveLogsAndEmail(stageName) {
    writeFile file: 'console-log.txt', text: currentBuild.rawBuild.getLog(1000).join('\n')
    emailext (
        subject: "${currentBuild.currentResult}: ${stageName}",
        body: "Please find the attached log for details of the ${stageName}.",
        attachmentsPattern: 'console-log.txt',
        to: "${env.EMAIL_RECIPIENT}"
    )
}
