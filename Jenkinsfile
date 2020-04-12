def gradle(command) {
    sh "./gradlew ${command}"
}

node {
  checkout scm
  gradle 'build'
}
	
