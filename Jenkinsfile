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
                    sh 'npm install'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'npm test'
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
                    sh '''
                    kubectl apply -f k8s/deployment.yaml
                    kubectl apply -f k8s/service.yaml
                    '''
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
}