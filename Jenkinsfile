pipeline {
    agent any
    environment {
        SONAR_TOKEN = credentials('sonar-token') // matches the Jenkins credential ID
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
                // Use withSonarQubeEnv if SonarQube server is configured in Jenkins
                withSonarQubeEnv('SonarQube-local') { // Name of SonarQube server in Jenkins
                    sh "./gradlew sonarqube -Dsonar.login=$SONAR_TOKEN -Dsonar.host.url=http://localhost:9000"
                }
            }
        }
    }
}
