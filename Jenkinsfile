pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'docker-credentials'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', url: 'https://github.com/Akash-879/node-express-hello-world'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    powershell 'npm install'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.withRegistry('', env.DOCKER_CREDENTIALS_ID) {
                        def appImage = docker.build('akash879/hellonode:latest')
                        appImage.push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    powershell '''
                    minkube start
                    kubectl apply -f k8s/deployment.yml
                    kubectl apply -f k8s/service.yml
                    '''
                }
            }
        }
    }
    post {
        success {
            mail to: 'rathodakash4615@gmail.com', subject: 'Pipeline Success', body: 'The deployment was successful.'
        }
        failure {
            mail to: 'rathodakash4615@gmail.com', subject: 'Pipeline Failure', body: 'The pipeline failed.'
        }
    }
}
