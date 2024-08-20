#!groovy
pipeline {
	agent none
	stages {
		stage('Maven Install') {
		    agent {
				docker {
					image 'maven:3.5.0'
					alwaysPull true
				}
			}
			steps {
			    sh 'pwd'
// 			    sh 'mvn --version'
// 				sh 'mvn clean install'
			}
		}
// 		stage('Build') {
//             steps {
//                 sh 'mvn -B -DskipTests clean package'
//             }
//         }
// 		stage('Docker Build') {
// 			agent any
// 			steps {
// 				sh 'docker build -t grupo02/spring-petclinic:latest .'
// 			}
// 		}
	}
}
