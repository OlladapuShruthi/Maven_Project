pipeline {
    agent any

    tools {
        maven 'MAVEN'
        jdk 'DefaultJDK'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                git url: 'https://github.com/OlladapuShruthi/Maven_Project.git', branch: 'master'
            }
        }

        stage('Build & Test') {
            steps {
                echo 'Running Maven build and tests...'
                bat 'mvn clean test'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the project...'
                bat 'mvn clean package'
            }
        }

        stage('Archive Artifact') {
            steps {
                echo 'Archiving the built JAR file...'
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
    }
}
