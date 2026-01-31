pipeline {
    agent any
    environment {
        SONAR_TOKEN = credentials('squ_05a92e0e88541fe9bc89fd947b8c48893df5ecf5') // matches the Jenkins credential ID
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
                withSonarQubeEnv('SonarQube-Local') { // Name of SonarQube server in Jenkins
                    sh "./gradlew sonarqube -Dsonar.login=$SONAR_TOKEN -Dsonar.host.url=http://localhost:9000"
                }
            }
        }
    }
}
