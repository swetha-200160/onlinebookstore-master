pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Repository cloned'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                bat 'mvn sonar:sonar'
            }
        }
    }
}