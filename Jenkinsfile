pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    environment {
        SONARQUBE_ENV = 'sonarqube-server'
    }

    stages {
        stage('Clone Git Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/ryn4455/school.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'sonarscanner'
            }
            steps {
                withSonarQubeEnv("${SONARQUBE_ENV}") {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t school-app:latest .'
            }
        }
    }
}
