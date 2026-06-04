pipeline {
    agent any

    tools {
        maven 'Maven-3.9.16'
    }

    environment {
        SONAR_HOST_URL = 'http://localhost:9000'
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/swetha-200160/onlinebookstore-master.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                    bat "mvn sonar:sonar -Dsonar.host.url=%SONAR_HOST_URL% -Dsonar.token=%SONAR_TOKEN%"
                }
            }
        }

        stage('Deploy to Nexus') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'nexus-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat 'mvn deploy -Dnexus.username=%USER% -Dnexus.password=%PASS%'
                }
            }
        }
    }
}