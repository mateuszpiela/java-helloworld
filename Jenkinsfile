pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',url: 'https://git.horizonnet.eu/mateusz/java-helloworld.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
                junit '**/target/surefire-reports/*.xml'
                recordCoverage(tools: [[parser: 'JACOCO']], id: 'jacoco', name: 'JaCoCo Coverage', sourceCodeRetention: 'EVERY_BUILD')
            }
        }
        stage('Deploy') {
            steps {
                sh 'mvn package'
                archiveArtifacts artifacts: 'target/helloworld*.jar', fingerprint: true
            }
        }
    }
}