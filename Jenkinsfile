pipeline {
    agent any

    stages {
        stage('Deploy to k8s') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: ' EKS-1', contextName: 'webapps', credentialsId: 'k8-token', namespace: '', serverUrl: 'https://C77C48DAE963882A4948A8D50D29015B.yl4.eu-west-2.eks.amazonaws.com']]) {
     sh "kubectl apply -f deployment-service.yml"
     sleep 60
            }
            }
        }
        
        stages {
        stage('Verify Deployment') {
            steps {
               withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: ' EKS-1', contextName: 'webapps', credentialsId: 'k8-token', namespace: '', serverUrl: 'https://C77C48DAE963882A4948A8D50D29015B.yl4.eu-west-2.eks.amazonaws.com']]) {
     sh "kubectl get all -n webapps"
            }
            }
        }
    }
}
