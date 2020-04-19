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
                scannerHome = tool 'MySonarScanner'
            }
            steps {
                sh 'echo $scannerHome'
                withSonarQubeEnv('MySonar') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage('War'){
            steps{
                sh './gradlew build'
            }
        }
        stage('Docker'){
            steps {
                sh 'docker build -t springapp:1.0 .'
            }
        }
    }
}