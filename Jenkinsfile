pipeline {
	agent none
	stages {
		stage('Maven Install') {
			agent {
				docker {
					image 'maven:3.9.0'
					args '-v /tmp/.m2:/root/.m2'
				}
			}
			steps {
				sh 'mvn clean'
				sh 'mvn test install -U'
			}
			post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
		}
		stage('Docker Build') {
			agent any
				steps {
				sh 'docker build -t grupo02/spring-petclinic:latest .'
			}
		}
	}
}
