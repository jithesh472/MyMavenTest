pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'checkout successfull'
            }
        }
        stage('Build') {
            steps {
                script {
                    checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'jit', url: 'https://github.com/jithesh472/MyMavenTest.git']])
                }
            }
        }
        stage('Unit Test') {
            steps {
                echo 'Unit test successfull'
            }
        }
        stage('Security Scan') {
           steps {
                echo 'Security scan successfull'
            }
        }
         
    }

}