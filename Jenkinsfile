pipeline {
  agent any
  stages {
    stage('Docker Build') {
      steps {
        sh "docker build -t sarathi850/first:${env.BUILD_NUMBER} ."
      }
    }
    stage('Docker Push') {
      steps {
        withCredentials([string(credentialsId: 'DOCKER_HUB', variable: 'DOCKER_HUB')]) {
         // some block
         }
          sh "docker push sarathi850/first:${env.BUILD_NUMBER}"
        }
      }
    stage('Docker Remove Image') {
      steps {
        sh "docker rmi sarathi850/first:${env.BUILD_NUMBER}"
      }
    }
    stage('Apply Kubernetes Files') {
      steps {
          withKubeConfig([credentialsId: 'KUBERNETES_CLUSTER_CONFIG']) {
          sh 'cat deployment.yaml | sed "s/{{BUILD_NUMBER}}/$BUILD_NUMBER/g" | kubectl apply -f -'
          sh 'kubectl apply -f service.yaml'
        }
      }
  }
}
post {
    success {
      slackSend(message: "Pipeline is successfully completed.")
    }
    failure {
      slackSend(message: "Pipeline failed. Please check the logs.")
    }
}
}
