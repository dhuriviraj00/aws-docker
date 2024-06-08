pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }

        stage('Git Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHub-id', url: 'https://github.com/dhuriviraj00/aws-docker.git']]])
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t test .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove any existing container with the same name
                    sh 'docker stop test || true'
                    sh 'docker rm test || true'

                    // Run a new container with port mapping
                    sh 'docker run -d -p 5000:80 --name test test'
                }
            }
        }
    }
}
