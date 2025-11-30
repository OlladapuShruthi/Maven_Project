pipeline {
    agent any

    tools {
        jdk 'DefaultJDK'    // Make sure JDK is configured in Jenkins global tools
        maven 'MAVEN'       // Make sure Maven is configured in Jenkins global tools
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/OlladapuShruthi/Maven_Project.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished'
        }
        success {
            mail bcc: '', body: 'Build Success', cc: '', from: '', replyTo: '', subject: 'Jenkins Build Success', to: 'olladapushruthi@gmail.com'
        }
        failure {
            mail bcc: '', body: 'Build Failed', cc: '', from: '', replyTo: '', subject: 'Jenkins Build Failed', to: 'olladapushruthi@gmail.com'
        }
    }
}
