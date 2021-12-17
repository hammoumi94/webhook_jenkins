node {
     stage('Clone sources') {
           git 'https://github.com/hammoumi94/webhook_jenkins.git'
        }
     stage('Build') {
           sh label: '', script: 'javac Main.java'
                }
     stage('Run') {
           sh label: '', script: 'java Main'
                }
     stage('SonarQube analysis') {
	   def scannerHome = tool 'sonarqubetest'
	        withSonarQubeEnv('sonar'){
	               sh "${scannerHome}/bin/sonar-scanner -Dsonar.host.url=http://127.0.0.1:9000 -Dsonar.projectName=sonarqubetest -Dsonar.projectVersion=${env.BUILD_NUMBER} -Dsonar.projectKey=sonarqubetest  -Dsonar.sources=./ -Dsonar.language=java -Dsonar.java.binaries=."
	        }
	    }
	
     stage('Gate Quality'){
	        def qualitygate = waitForQualityGate()
	        if (qualitygate.status != "OK") {
	                error "Pipeline aborted due to quality gate coverage failure: ${qualitygate.status}"
	        }
	    }

}
