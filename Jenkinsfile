pipeline {
    agent any

    tools {
        jdk 'DefaultJDK'       // Make sure this matches the JDK name in Jenkins
        maven 'MAVEN'          // Make sure this matches the Maven name in Jenkins
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
                echo 'Running Maven clean and test...'
                bat 'mvn clean test'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the project...'
                bat 'mvn package'
            }
        }

        stage('Archive Artifact') {
            steps {
                echo 'Archiving the built JAR file...'
                // Use wildcard to catch any JAR in target folder
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
    }
}
