pipeline {
    agent none
    stages {
        stage('Prepare Cache') {
            agent {
                docker {
                    image 'maven:3.5.0'
                    reuseNode true
                }
            }
            steps {
                script {
                    // Restore cache if exists
                    def cacheDir = '.m2/repository'
                    if (fileExists(cacheDir)) {
                        echo "Restoring cache..."
                        sh "cp -r ${cacheDir} \$HOME/.m2/"
                    }
                }
            }
        }
        stage('Maven Install') {
            agent {
                docker {
                    image 'maven:3.5.0'
                    reuseNode true
                }
            }
            steps {
                sh 'mvn clean install'
                script {
                    // Save cache
                    def cacheDir = '.m2/repository'
                    sh "cp -r \$HOME/.m2/ ${cacheDir}"
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
