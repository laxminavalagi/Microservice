pipeline {
    agent any

    environment {
        K8S_CREDENTIALS_ID = 'k8-token'
        K8S_CLUSTER_URL = 'https://9F39F577334FF23706994135261985F2.gr7.ap-south-1.eks.amazonaws.com'
        K8S_NAMESPACE = 'webapps'
    }

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeConfig(
                    credentialsId: "${K8S_CREDENTIALS_ID}",
                    serverUrl: "${K8S_CLUSTER_URL}",
                    namespace: "${K8S_NAMESPACE}"
                ) {
                    sh "kubectl apply -f deployment-service.yml"
                }
            }
        }
        
        stage('Verify Deployment') {
            steps {
                withKubeConfig(
                    credentialsId: "${K8S_CREDENTIALS_ID}",
                    serverUrl: "${K8S_CLUSTER_URL}",
                    namespace: "${K8S_NAMESPACE}"
                ) {
                    sh "kubectl get svc -n ${K8S_NAMESPACE}"
                }
            }
        }
    }
}
