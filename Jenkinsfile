pipeline {
  agent any
  tools { 
        maven 'Maven_17.0.18'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=makemoney -Dsonar.organization=makemoney -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=5e1e864a987d68a4dc91d174cf4b8e15849419bf'
			}
    }

	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }		
  }
}
