#!groovy
pipeline {
	agent none
	stages {
		stage('Maven Install') {
		echo 'Maven Install..'
		agent {
				docker {
					image 'maven:3.5.0'
				}
			}
			steps {
				sh 'mvn clean install'
			}
		}
		stage('Docker Build') {
		echo 'Docker Build..'
			agent any
			steps {
				sh 'docker build -t grupo02/spring-petclinic:latest .'
			}
		}
	}
}
