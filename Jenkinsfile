pipeline {
  agent any
  stages {
    stage('Apply Kubernetes Files') {
      steps {
        withCredentials([kubeconfigFile(credentialsId: 'KUBERNETES_CLUSTER_CONFIG', variable: 'KUBECONFIG')]) {
    // some block
}
         
          sh 'kubectl create -f https://k8s.io/examples/application/deployment.yaml'
  }
    }
}
}

