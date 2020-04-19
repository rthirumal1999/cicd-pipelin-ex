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
                stagecannerHome = tool 'MySonarScanner'
            }
            steps {
                withSonarQubeEnv('MySonar') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}