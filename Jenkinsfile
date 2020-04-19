pipeline {
    agent any
    stages {
        stage('Compile'){
            steps {
                sh "./gradlew compileJava"
            }
        }
        stage('Junit'){
            steps {
                sh "./gradlew test"
            }
        }
        stage('Sonar'){
            environment {
                stagecannerHome = tool 'MySonar'
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