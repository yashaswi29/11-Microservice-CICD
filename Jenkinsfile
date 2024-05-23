pipeline {
    agent any

    stages {
        stage('Deploying to EKS') {
            steps {
                withCredentials([kubeconfigFile(credentialsId: 'k8-token', variable: 'KUBECONFIG')]) {
                    sh '''
                        export TOKEN=$(kubectl get secret $(kubectl get serviceaccount default -o jsonpath='{.secrets[0].name}') -n webapps -o jsonpath='{.data.token}' | base64 -d)
                        kubectl apply -f deployment-service.yml --token="${TOKEN}" 
                    '''
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
