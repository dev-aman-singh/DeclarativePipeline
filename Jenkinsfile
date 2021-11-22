pipeline {
	agent any
	stages {
		stage('cleaning stage'){
			steps {
			   bat "mvn clean"
			}
		}
		stage('Testing stage'){
			steps {
			   bat "mvn test"
			}
		}	
	       stage('Packaging stage'){
			steps {
			   bat "mvn package"
			}
		}
		
		stage("Consolidate Results") {
			steps {
				input ("Do you want to capture results?")
				junit '**/target/surefire-reports/TEST-*.xml'
				archiveArtifacts artifacts: 'target/*.jar'
			}
		}
		
		stage("Deploy on Production")
		{
		  steps{
		    echo "deploying on Production or Container"
			deploy adapters: [tomcat9(credentialsId: 'c635b8c3-0a1e-4828-bde6-9f26edb38949', path: '', url: 'http://localhost:8080')], contextPath: '/deployment', war: '**/*.war'
		  }
		}
		
		
		
		stage("Email Build Status"){
			steps {
				mail body: "${env.JOB_NAME}  - Build # ${env.BUILD_NUMBER}  - ${currentBuild.currentResult} \n\nCheck console output at ${env.BUILD_URL} to view the results.", subject: "${env.JOB_NAME}  - Build # ${env.BUILD_NUMBER}  - ${currentBuild.currentResult}!!", to: 'amansingh1031997@gmail.com'
			}
		}
		
	}
}

