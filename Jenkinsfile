pipeline {
  agent any
  stages {
    stage('Docker Build') {
      steps {
        sh "docker build -t sarathi850/helloworld:${env.BUILD_NUMBER} ."
      }
    }
    stage('Docker Push') {
      steps {
          sh "docker login -u sarathi850 -p Partha@108"
          sh "docker push sarathi850/helloworld:${env.BUILD_NUMBER}"
      }
    }
    stage('Docker Remove Image') {
      steps {
        sh "docker rmi sarathi850/helloworld:${env.BUILD_NUMBER}"
      }
    }
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

