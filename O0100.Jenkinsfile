pipeline {
  agent {
        kubernetes {
        label 'alpine'
        yamlFile 'build-pod.yaml'
        defaultContainer 'alpine'
        }
    }
  stages {
    stage("Run docker") {
      steps {
        container('alpine') {
          sh 'ls'
          sh 'helm version --client'
          sh 'kubectl config view'
          sh 'helm repo add bitnami https://charts.bitnami.com/bitnami'
          sh 'helm upgrade --install nginx bitnami/nginx'
        }
      }
    }
  }
}

