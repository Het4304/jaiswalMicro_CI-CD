pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'kubernetes', contextName: 'kubernetes-admin@kubernetes', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://10.128.0.10:6443']]) {
                    sh "kubectl apply -f deployment-service.yml"
                    
                }
            }
        }
        
        stage('verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'kubernetes', contextName: 'kubernetes-admin@kubernetes', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://10.128.0.10:6443']]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
