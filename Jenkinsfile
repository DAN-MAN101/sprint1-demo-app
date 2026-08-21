pipeline {
    agent any
    stages {
        stage('Diagnose') {
            steps {
                sh 'java -version'
                sh 'echo JAVA_HOME=$JAVA_HOME'
                sh 'which java'
                sh 'which javac'
                sh 'javac -version'
                sh 'mvn -version'
            }
        }
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn -B test'
            }
            post {
                always {
                    junit 'target/test-reports/*.xml'
                }
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
