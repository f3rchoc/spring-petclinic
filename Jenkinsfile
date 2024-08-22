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
                sh 'mvn clean install'
//                 sh 'mvn test -DfailIfNoTests'
            }
        }
        stage ('Maven test') {
            agent any
//              agent {
//                 docker {
//                     image 'maven:3.5.0'
//                 }
//             }
            steps {
                sh 'mvn test -DfailIfNoTests'
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
