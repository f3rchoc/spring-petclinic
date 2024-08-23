pipeline {
    agent {
        docker {
            image 'maven:3.9.0'
            args '-v /tmp/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
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
//         stage('Deliver') {
//             steps {
//                 sh './jenkins/scripts/deliver.sh'
//             }
//         }
    }
}
