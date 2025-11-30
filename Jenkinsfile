pipeline {
    agent any

    tools {
        jdk 'DefaultJDK'
        maven 'MAVEN'
    }

    environment {
        // Optional: Email recipient
        EMAIL_RECIPIENT = 'olladapushruthi@gmail.com'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/OlladapuShruthi/Maven_Project.git'
            }
        }

        stage('Build & Test') {
            steps {
                // Windows batch command
                bat 'mvn clean test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Build completed'
        }

        success {
            // Publish test results
            junit '**/target/surefire-reports/*.xml'

            // Optional: Send email (requires Email Extension Plugin)
            mail to: "${EMAIL_RECIPIENT}",
                 subject: "SUCCESS: Maven_Project Build #${env.BUILD_NUMBER}",
                 body: "Good news! The build succeeded. Check console output: ${env.BUILD_URL}"
        }

        failure {
            junit '**/target/surefire-reports/*.xml'
            mail to: "${EMAIL_RECIPIENT}",
                 subject: "FAILURE: Maven_Project Build #${env.BUILD_NUMBER}",
                 body: "Oops! The build failed. Check console output: ${env.BUILD_URL}"
        }
    }
}
