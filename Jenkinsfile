pipeline {
    agent none
    stages {
        stage('Maven Install') {
            agent {
                docker {
                    image 'maven:3.5.0'
                    reuseNode true
                }
            }
            steps {
                // Cache Maven dependencies
                cache(path: '.m2/repository', key: 'maven-dependencies') {
                    sh 'mvn clean install'
                }
            }
        }
        stage('Maven Test') {
            agent {
                docker {
                    image 'maven:3.5.0'
                    reuseNode true
                }
            }
            steps {
                // Reuse cached Maven dependencies
                cache(path: '.m2/repository', key: 'maven-dependencies') {
                    sh 'mvn test -DfailIfNoTests'
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
