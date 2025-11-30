pipeline {
    agent any

    tools {
        jdk 'DefaultJDK'
        maven 'MAVEN'
    }

    environment {
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
            junit '**/target/surefire-reports/*.xml'
            mail to: "${EMAIL_RECIPIENT}",
                 subject: "SUCCESS: Maven_Project Build #${env.BUILD_NUMBER}",
                 body: "Good news! Build succeeded. ${env.BUILD_URL}"
        }

        failure {
            junit '**/target/surefire-reports/*.xml'
            mail to: "${EMAIL_RECIPIENT}",
                 subject: "FAILURE: Maven_Project Build #${env.BUILD_NUMBER}",
                 body: "Oops! Build failed. ${env.BUILD_URL}"
        }
    }
}
