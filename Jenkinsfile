pipeline {
    agent any

    environment {
        AWS_REGION = 'eu-west-2'
        CLUSTER_NAME = 'EKS-1'
        NAMESPACE = 'webapps'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Deploy To Kubernetes') {
            steps {
                // Configure kubeconfig dynamically for EKS
                sh '''
                    aws eks --region $AWS_REGION update-kubeconfig --name $CLUSTER_NAME
                    kubectl apply -f deployment-service.yml -n $NAMESPACE
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                    aws eks --region $AWS_REGION update-kubeconfig --name $CLUSTER_NAME
                    kubectl get pods -n $NAMESPACE
                    kubectl get svc -n $NAMESPACE
                '''
            }
        }
    }
}
