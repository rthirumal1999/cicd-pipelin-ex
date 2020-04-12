pipeline {
  agent any 
    stages {
      stage ('Git..'){
        steps {
          sh 'echo I am fine'
          def GRADLE_HOME = tool name: 'gradle', type: 'hudson.plugins.gradle.GradleInstallation'
          sh 'echo ${GRADLE_HOME}'
          sh "${GRADLE_HOME}/bin/gradle build"
          sh 'echo built'
        }
      }
    }
}

	
