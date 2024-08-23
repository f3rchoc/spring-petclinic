pipeline {
    agent none
    environment {
        CACHE_DIR = '/home/.m2/repository'
    }
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
                    if (fileExists(env.CACHE_DIR)) {
                        echo "Restoring cache..."
                        sh "cp -r ${env.CACHE_DIR} \$HOME/.m2/"
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
                    sh "cp -r \$HOME/.m2/ ${env.CACHE_DIR}"
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
        stage('Cleanup Cache') {
            agent any
            steps {
                script {
                    if (fileExists(env.CACHE_DIR)) {
                        echo "Cleaning up cache..."
                        sh "rm -rf ${env.CACHE_DIR}"
                    }
                }
            }
        }
    }
}
