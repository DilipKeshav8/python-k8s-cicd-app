pipeline {
  agent any

    environment {
        KUBECONFIG = "/root/.kube/config"
        DOCKER_IMAGE = "dilipkeshav8/python-k8s-app:${BUILD_NUMBER}"
    }

    stages {
        stage('Clone') {
            steps {
                // Clone your GitHub repo
                git branch: 'main', url: 'https://github.com/DilipKeshav8/python-k8s-cicd-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build Docker image with unique tag per build number
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                // Login to Docker Hub securely and push image
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
                // Update the deployment manifest image tag and deploy to K8s cluster
                sh '''
                    sed -i "s|image:.*|image: $DOCKER_IMAGE|g" Kubernetes/deployment.yaml
                    kubectl apply -f Kubernetes/deployment.yaml
                    kubectl apply -f Kubernetes/service.yaml
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment successful! App deployed with image: $DOCKER_IMAGE"
        }
        failure {
            echo "Deployment failed. Check logs for details."
        }
    }
}
