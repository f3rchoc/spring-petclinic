pipeline {
    agent none
    stages {
        stage('Maven Install') {
            agent {
                docker {
                    image 'maven:3.5.0'
                }
            }
            steps {
                sh 'mvn clean'
            }
        }
        stage ('Maven test') {
            steps {
                sh 'mvn test'
            }
        }
        stage ('Maven build') {
            steps {
                sh 'mvn install -DskipTests'
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
