pipeline {
  agent any
  tools { 
        maven 'Maven_3_2_5'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=ciphersecio-sast -Dsonar.organization=ciphersecio-sast -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=54b4e5135e28fb8936ac60b48e825aeb491d0adb'
			}
        } 
  }
}
