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
		
	}
}
