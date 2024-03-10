pipeline {
    agent any

    stages {
        stage('Checkout') {
            git branch: 'master',url: 'https://git.horizonnet.eu/mateusz/java-helloworld.git'
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
                jacoco 
            }
        }
        stage('Deploy') {
            steps {
                sh 'mvn package'
                archiveArtifacts artifacts: '***/target/*.jar', fingerprint: true
            }
        }
    }
}