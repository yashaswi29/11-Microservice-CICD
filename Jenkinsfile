pipeline {
    agent any

    stages {
        stage('Deploying to EKS') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-2', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://7D11FCC3F3B02B9F5ABDE7D1C2EC8453.gr7.ap-south-1.eks.amazonaws.com']]) {
                    sh "git --version --verbose"
                    sh "kubectl apply --v=8 -f deployment-service.yml"

                    // sh "kubectl apply -f deployment-service.yml"
                }
            }
        }
        stage('Verifiying Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-2', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://7D11FCC3F3B02B9F5ABDE7D1C2EC8453.gr7.ap-south-1.eks.amazonaws.com']]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
