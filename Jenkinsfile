pipeline {
  agent any
  stages {
    stage('Apply Kubernetes Files') {
      steps {
        withCredentials([kubeconfigFile(credentialsId: 'KUBERNETES_CLUSTER_CONFIG', variable: 'KUBECONFIG')]) {
    // some block
}
         
          sh 'kubectl apply -f kubernetes-manifest.yaml'
  }
    }
}
}

