pipeline {
	agent any
	
    stages {
		stage('Compile Code') {
			steps {
				dir('C:\\repositorios\\ejemplo-maven'){
				sh "./mvnw.cmd clean compile -e"
				}
			}
		}
		stage('Test Code') {
			steps {
				dir('C:\\repositorios\\ejemplo-maven'){
				sh "./mvnw.cmd clean test -e"
				}
			}
		}
		stage('Jar Code') {
			steps {
				dir('C:\\repositorios\\ejemplo-maven'){
				sh "./mvnw.cmd clean package -e"
				}
			}
		}
		stage('Run Jar') {
			steps {
				dir('C:\\repositorios\\ejemplo-maven'){
				sh "./mvnw.cmd spring-boot:run"
				}
			}
		}
	    	stage('sonarQube') {
			steps {
				dir('C:\\repositorios\\ejemplo-maven'){
				withSonarQubeEnv('sonar') { 
				      sh './mvnw org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
				    }
				}
			}
		}
		stage('Testing Application') {
			steps {
				dir('C:\\repositorios\\ejemplo-maven'){
				sh "start chrome http://localhost:8081/rest/mscovid/test?msg=testing"
				}
			}
		}
	}
}
