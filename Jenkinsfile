pipeline {
  agent any
  stages {
    stage('Docker Build') {
      steps {
        sh "docker build -t sarathi850/class:${env.BUILD_NUMBER} ."
      }
    }
    stage('Docker Push') {
      steps {
          sh "docker login -u sarathi850 -p Partha@108"
          sh "docker push sarathi850/class:${env.BUILD_NUMBER}"
      }
    }
    stage('Docker Remove Image') {
      steps {
        sh "docker rmi sarathi850/class:${env.BUILD_NUMBER}"
      }
    }
    stage('Apply Kubernetes Files') {
      steps {
          kubernetesdeploy(
                  configs: 'deployment.yaml',
                  kubeconfigid: 'KUBERNETES_CLUSTER_CONFIG',
                  enableConfigSubstitution: true
          )
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
}
