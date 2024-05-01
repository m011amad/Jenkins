pipeline {
    agent any
    environment {
        EMAIL_RECIPIENT = 's223632922@deakin.edu.au'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build - In this stage, the source code is compiled and packaged into an executable or deployable artifact. Tool used: Maven for Java projects, which automates the build lifecycle and dependencies.'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Unit and Integration Tests - This stage runs automated tests to validate the integrity and correctness of the code. For unit testing, JUnit is used to test individual components; for integration testing, TestNG could be used to handle test suites and groups.'
            }
            post {
                always {
                    script {
                        // Save the last 1000 lines of the log to a file
                        writeFile file: 'console-log.txt', text: currentBuild.rawBuild.getLog(1000).join('\n')
                    }
                    emailext (
                        subject: "${currentBuild.currentResult}: Unit and Integration Tests",
                        body: "Please find the attached log for details of the test execution.",
                        attachmentsPattern: 'console-log.txt',
                        to: "${env.EMAIL_RECIPIENT}"
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Analysis - Automated code analysis is performed to ensure code quality and adherence to coding standards. Tools like SonarQube can be used here to perform static code analysis, highlighting potential issues and technical debt.'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan - Security vulnerabilities within the code are identified and reported. Tools such as OWASP ZAP can be used for dynamic application security testing (DAST) to simulate attacks on the application.'
            }
            post {
                always {
                    script {
                        // Save the last 1000 lines of the log to a file
                        writeFile file: 'console-log.txt', text: currentBuild.rawBuild.getLog(1000).join('\n')
                    }
                    emailext (
                        subject: "${currentBuild.currentResult}: Security Scan",
                        body: "Please find the attached log for details of the security scan.",
                        attachmentsPattern: 'console-log.txt',
                        to: "${env.EMAIL_RECIPIENT}"
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to Staging - The built and tested application is deployed to a staging environment, which mimics the production environment. This is crucial for further testing and client reviews. Tools like Jenkins Deployment plugins or AWS CodeDeploy can be used to automate this process.'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging - Additional integration tests are conducted in the staging environment to ensure the application operates as expected under conditions that closely simulate the production environment. Selenium can be used here for web application testing.'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production - Finally, the application is deployed to the production server where it becomes available to end users. This can be automated using tools like Jenkins or through specific deployment tools like AWS CodeDeploy, depending on the hosting environment.'
            }
        }
    }
}
