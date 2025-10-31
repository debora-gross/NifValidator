# !groovy

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

    }
}

/*pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo "Building the project..."'
                // Add your build commands here
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
                // Add your test commands here
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "Deploying to production..."'
                // Add your deployment commands here
            }
        }
    }
}*/

