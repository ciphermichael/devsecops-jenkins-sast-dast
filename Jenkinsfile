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
      stage('RunSCAAnalysisUsingSnyk') {
            steps {
                  withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
                        sh 'mvn snyk:test -fn'
                  }
            }
      }
      stage('Build') {
            steps {
                  withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
                        script{
                              app = docker.build("asg")
                        }
                  }
            }
      }
      stage('Push') {
            steps {
                  script{
                        docker.withRegistry('https://362895328443.dkr.ecr.eu-west-1.amazonaws.com', 'ecr:eu-west-1:aws-credentials'){
                              app.push("lastest")
                        }
                  }
            }
      }
  }
}
