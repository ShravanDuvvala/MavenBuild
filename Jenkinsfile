node('') {
	stage ('checkout code'){
		checkout scm
	}
	
	stage ('Build'){
		sh "mvn clean install -Dmaven.test.skip=true"
	}

	stage ('Test Cases Execution'){
		sh "mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
	}

	stage ('Archive Artifacts'){
		archiveArtifacts artifacts: 'target/*.war'
	}
	

	stage ('Deployment'){
		deploy adapters: [tomcat9(credentialsId: 'TomcatCreds', path: '', url: 'http://3.84.47.228:8080/')], contextPath: 'counterwebapp', war: 'target/*.war'
	}
	

	stage ('Notification'){
		emailext (
		      subject: "Job Completed",
		      body: "Jenkins Pipeline Job for Maven Build got completed !!!",
		      to: "build-alerts@example.com"
		    )
	}
}
