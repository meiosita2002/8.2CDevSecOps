pipeline {
    agent any

    triggers {
        pollSCM('H/5 * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building the code using Maven to compile and package the application"
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests and integration tests using JUnit and TestNG"
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Analysing code quality and maintainability using SonarQube"
            }
        }

        stage('Security Scan') {
            steps {
                echo "Scanning the code for security vulnerabilities using OWASP Dependency-Check"
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to a staging server (AWS EC2 instance)"
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on the staging environment to verify production-like behaviour"
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying the application to the production server (AWS EC2 instance)"
            }
        }
    }
}
