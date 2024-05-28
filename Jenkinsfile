pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/MyuriAnily/todo-app.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    docker.build('viruko/todo-app:latest')
                }
            }
        }

        stage('Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image('viruko/todo-app:latest').push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}