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
				sleep(time: 10, unit: "SECONDS")
				dir('C:\\repositorios\\ejemplo-maven'){
				sh "./mvnw.cmd spring-boot:run"
				}
			}
		}
		stage('Nexus Upload'){
                    steps {
                        nexusArtifactUploader(
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        nexusUrl: 'localhost:8081',
                        groupId: 'com.devopsusach2020',
                        version: '0.0.1',
                        repository: 'test-nexus',
                        credentialsId: 'nexus-local',
                        artifacts: [
                            [artifactId: 'DevOpsUsach2020',
                            classifier: '',
                            file: 'C:/repositorios/ejemplo-maven/build/DevOpsUsach2020-0.0.1.jar',
                            type: 'jar']
                        ]
                    )
                        }
                }
	}
}
