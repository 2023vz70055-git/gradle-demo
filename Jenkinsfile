pipeline {
    agent any

    tools {
        gradle 'Gradle_7'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/2023vz70055-git/gradle-demo.git'
            }
        }

        stage('Build & Test') {
            steps {
                sh './gradlew clean build jacocoTestReport'
            }
        }

        stage('SonarQube Analysis') {
            environment {
                SONAR_TOKEN = credentials('sonar-token') // Replace with your Jenkins SonarQube token ID
            }
            steps {
                withSonarQubeEnv('MySonarQube') { // Replace with your SonarQube installation name in Jenkins
                    sh "./gradlew sonarqube -Dsonar.login=$SONAR_TOKEN"
                }
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
