pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh "docker build -t zakyfatih/python-program:latest ."
            }
        }
        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-zaky', passwordVariable: 'pass', usernameVariable: 'user')]) {
                    sh 'docker login -u $user --password $pass'
                    sh 'docker push zakyfatih/python-program:latest'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'minikube service python-service'
            }
        }
    }
}
    