pipeline {
  agent any

  tools {
    // Name of Maven installation in Jenkins global config
    maven 'MAVEN'  
    // Name of JDK installation in Jenkins global config
    jdk 'DefaultJDK'  
  }

  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/OlladapuShruthi/WebProject.git', branch: 'master'
      }
    }

    stage('Build & Test') {
      steps {
        // Build and run tests
        sh 'mvn clean test'
      }
    }

    stage('Package') {
      steps {
        // Build the WAR (or package accordingly)
        sh 'mvn clean package'
      }
    }

    stage('Archive Artifact') {
      steps {
        // Archive the WAR/JAR artifact produced
        archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
      }
    }

    // Optional: deploy to Tomcat if you have a server ready
    // stage('Deploy to Tomcat') {
    //   steps {
    //     // For example, copy WAR to Tomcat webapps directory
    //     sh 'cp target/yourapp.war /path/to/tomcat/webapps/'
    //   }
    // }
  }

  post {
    always {
      // (optional) record test results, if you have surefire reports
      junit '**/target/surefire-reports/*.xml'
    }
  }
}
