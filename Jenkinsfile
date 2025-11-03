#!groovy

pipeline {
    agent any
    environment {
        HOME = "${env.WORKSPACE}"
    }

    stages {
        stage('Docker environment') {
            agent {
                docker {
                    image 'python:3.11-slim'
                    reuseNode true
                }
            }
            steps {
                sh"""
                pip install -r requirements.txt
                """
            }
        }

        stage('Deliver') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId:'docker-debora', 
                    passwordVariable:'passwd', 
                    usernameVariable:'username')]) {
                        sh """
                        printenv
                        docker build -t ${username}/nifvalidator .
                        docker login -u ${username} -p ${passwd}
                        docker push ${username}/nifvalidator
                        """
                    }
            }
        }

        stage('Deploy') {
            steps {
                sh """
                ssh redhat@172.31.45.135 docker --version
                """
            }
        }
    }
}
