#!groovy
pipeline {
	agent any
	stages {
		stage('Maven Install') {
		    agent {
				docker {
					image 'maven:3.5.0'
					alwaysPull true
					reuseNode true
				}
			}
			steps {
				sh 'mvn clean install'
			}
		}
// 		stage('Build') {
//             steps {
//                 sh 'mvn -B -DskipTests clean package'
//             }
//         }
		stage('Docker Build') {
			agent any
			steps {
				sh 'docker build -t grupo02/spring-petclinic:latest .'
			}
		}
	}
}
