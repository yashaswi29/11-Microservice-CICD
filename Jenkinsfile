pipeline {
    agent any

    stages {
        stage('Deploying to EKS') {
            steps {
                withKubeConfig([
                    credentialsId: 'k8-token', 
                    serverUrl: 'https://7D11FCC3F3B02B9F5ABDE7D1C2EC8453.gr7.ap-south-1.eks.amazonaws.com'
                ]) { 
                    sh "kubectl apply -f deployment-service.yml" 
                }
            }
        }
        stage('Verifying Deployment') {
            steps {
                withKubeConfig([
                    credentialsId: 'k8-token', 
                    serverUrl: 'https://7D11FCC3F3B02B9F5ABDE7D1C2EC8453.gr7.ap-south-1.eks.amazonaws.com'
                ]) { 
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
