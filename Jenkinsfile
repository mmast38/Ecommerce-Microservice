
pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
               withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: ' EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://C77C48DAE963882A4948A8D50D29015B.yl4.eu-west-2.eks.amazonaws.com']]) {
             sh "kubectl apply -f deployment-service.yml"
            }
            }
        }
        
        stage('verify Deployment') {
            steps {
               withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: ' EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://C77C48DAE963882A4948A8D50D29015B.yl4.eu-west-2.eks.amazonaws.com']]) {
    sh "kubectl get svc -n webapps"
}
            }
        }
    }
}
