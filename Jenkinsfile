pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/firaskhdhir11-lab/Jenkins-Demo.git'
            }
        }

        stage('Build App') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-service:$BUILD_NUMBER .'
            }
        }

        stage('Deploy Docker Container') {
            steps {
                sh 'docker rm -f devops-demo || true'
                sh 'docker run -d --name devops-demo -p 2223:2222 devops-service:$BUILD_NUMBER'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps --filter name=devops-demo'
            }
        }
    }

    post {
        success {
            echo 'Pipeline execution successful!'
        }
        failure {
            echo 'Pipeline execution failed.'
        }
    }
}
