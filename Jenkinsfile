pipeline {
    agent {
        docker {
            image 'maven:3.9.0'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}

// pipeline {
//     agent any
//     stages {
//         stage('Checkout') {
//             steps {
//                 checkout scm
//             }
//         }
//         stage('Build') {
//             steps {
//                 script {
//                     if (fileExists('build.gradle')) {
//                         sh './gradlew build'
//                     } else if (fileExists('pom.xml')) {
//                         sh 'mvn clean package'
//                     }
//                 }
//             }
//         }
//         stage('Unit Test') {
//             steps {
//                 script {
//                     sh 'mvn test' // or './gradlew test' for Gradle
//                 }
//             }
//             post {
//                 always {
//                     junit '**/target/surefire-reports/*.xml'
//                 }
//             }
//         }
//         stage('Security Scan') {
//             steps {
//                 veracode applicationName: 'YourAppName', scanType: 'Static'
//             }
//         }
//         stage('Deploy to Dev') {
//             steps {
//                 sh 'scp target/*.war user@dev-server:/path/to/tomcat/webapps/'
//             }
//         }
//     }
//     post {
//         failure {
//             mail to: 'developer@example.com',
//                 subject: "Build Failure: ${currentBuild.fullDisplayName}",
//                 body: "Check Jenkins for details."
//         }
//     }
// }