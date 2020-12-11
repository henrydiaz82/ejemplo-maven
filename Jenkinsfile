pipeline {
	agent any
    stages {
		stage('Compile Code') {
			steps {
				
				sh "./mvnw.cmd clean compile -e"
				}
			}		
		stage('Download') {
                    steps {
                            sh 'curl -X GET -u admin:admin http://localhost:8081/repository/test-nexus/com/devopsusach2020/DevOpsUsach2020/0.0.1/DevOpsUsach2020-0.0.1.jar -O'
                            sh 'pwd'
                    }
                }
		stage('Jar Code') {
			steps {
				
				sh "./mvnw.cmd clean package -e"
				
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
		stage('Run Jar') {
			steps {
				sleep(time: 10, unit: "SECONDS")
				
				sh "./mvnw.cmd spring-boot:run"
				
			}
		}
		
	}
}
