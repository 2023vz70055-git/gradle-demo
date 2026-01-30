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
                SONAR_TOKEN = credentials('squ_a493c2c5fdf005e86adfac1ed4bc8c9e7a16b26b') // Replace with your Jenkins SonarQube token ID
            }
                steps {
        sh "./gradlew sonarqube \
            -Dsonar.projectKey=gradle-demo \
            -Dsonar.host.url=http://localhost:9000 \
            -Dsonar.login=$SONAR_TOKEN"
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
