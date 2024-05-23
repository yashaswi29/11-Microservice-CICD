pipeline {
    agent any

    stages {
        stage('Deploy to Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-2', contextName: '', credentialsId: '', namespace: 'webapps', serverUrl: ' https://7D11FCC3F3B02B9F5ABDE7D1C2EC8453.gr7.ap-south-1.eks.amazonaws.com']]) {
                    sh "kubectl apply -f deployment-service.yml"
                    sleep 10
                }
            }
        }
            stage('Verify Deployement') {
                steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-2', contextName: '', credentialsId: '', namespace: 'webapps', serverUrl: ' https://7D11FCC3F3B02B9F5ABDE7D1C2EC8453.gr7.ap-south-1.eks.amazonaws.com']]) {
                        sh "kubectl get svc -n webapps"
                    }
            }
        }
    }
}
