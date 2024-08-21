// pipeline {
//     agent none
//     stages {
//         stage('Maven Install') {
//             agent {
//                 docker {
//                     image 'maven:3.5.0'
//             }
//         }
//         steps {
//         sh 'mvn clean install'
//         }
//         }
//         stage('Docker Build') {
//         agent any
//         steps {
//         sh 'docker build -t grupo02/spring-petclinic:latest .'
//         }
//         }
//     }
// }
pipeline {
    agent {
            docker {
                image 'maven:3.5.0'
            }
        }

        stages {
            stage("Build") {
                steps {
                    sh 'mvn -version'
                    sh 'mvn clean install'
                }
            }
        }

        post {
            always {
                cleanWs()
            }
        }
}
