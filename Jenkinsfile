pipeline {
    agent any

    tools {
        gradle 'Gradle_7'     // Replace with your Jenkins Gradle installation name
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/2023vz70055-git/gradle-demo.git'
            }
        }

        stage('Build & Test') {
            steps {
                // Linux/macOS agent
                sh './gradlew clean build'
                // Windows agent: use bat './gradlew.bat clean build'
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
