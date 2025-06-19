pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "dilipkeshav8/python-k8s-app:${BUILD_NUMBER}"
    }
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/DilipKeshav8/python-k8s-cicd-app.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push $DOCKER_IMAGE
                    '''
                }
            }
        }
        stage('Deploy to Kubernetes') {
    steps {
        sh '''
            sed -i "s|image:.*|image: $DOCKER_IMAGE|g" kubernetes/deployment.yaml
            kubectl apply -f kubernetes/deployment.yaml
            kubectl apply -f kubernetes/service.yaml
                '''
            }
        }
    }
}
