pipeline {
    agent any
    stages {
        stage('SCM') {
            scm checkout
        }
        stage('Compile'){
            sh "./gradlew compileJava"
        }
        stage('Junit'){
            sh "./gradlew test"
        }
        stage('Sonar'){
            environment {
                stagecannerHome = tool 'SonarQubeScanner'
            }
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}