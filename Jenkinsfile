pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonar-token')
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/2023vz70055-git/gradle-demo.git', branch: 'main'
            }
        }

        stage('Build & Test') {
            steps {
                sh './gradlew clean build jacocoTestReport'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube-Local') {
                    sh './gradlew sonarqube'
                }
            }
        }
    }
}
