node {
     stage('Clone sources') {
           git url: 'https://github.com/hammoumi94/webhook_jenkins.git'
        }

     stage('SonarQube analysis') {
           withSonarQubeEnv('SonarQube') {
               sh "./gradlew sonarqube"
        	}
	}
     stage("Quality gate") {
           waitForQualityGate abortPipeline: true
            }
     stage('Build') {
	   sh label: '', script: 'javac Main.java'
		}
     stage('Run') {
	   sh label: '', 'script: 'java Main'	
	        }

}
