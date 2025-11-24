// pipeline {
//     agent any

//     tools {
//         maven 'MAVEN_HOME'
//         jdk 'JAVA_HOME'
//     }

//     stages {
//         stage('Clone') {
//             steps {
//                 git 'https://github.com/OlladapuShruthi/Maven_Project.git'
//             }
//         }

//         stage('Build') {
//             steps {
//                 sh 'mvn clean install'
//             }
//         }

//         stage('Test') {
//             steps {
//                 sh 'mvn test'
//             }
//         }
//     }

//     post {
//         success {
//             echo "🎉 Pipeline completed successfully!"
//         }
//         failure {
//             echo "❌ Something went wrong."
//         }
//     }
// }
pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/OlladapuShruthi/Maven_Project.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
    }

    post {
        success {
            echo "🎉 BUILD SUCCESS — Java project compiled and tested!"
        }
        failure {
            echo "❌ Build failed — check console logs!"
        }
    }
}
