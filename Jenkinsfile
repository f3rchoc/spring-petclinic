#!groovy
pipeline {
	agent none
	stages {
		stage('Maven Install') {
		agent {
				docker {
					image 'maven:3.5.0'
					args '-v /var/run/docker.sock:/var/run/docker.sock'
				}
			}
			steps {
			    sh 'pwd'
			    sh 'mvn --version'
				sh 'mvn clean install'
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
