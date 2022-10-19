pipeline {
  agent {
    kubernetes {
      defaultContainer 'alpine'
      label 'alpine'
      yaml '''
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: alpine
  name: alpine
spec:
  containers:
  - name: alpine
    image: bsgrd/jenkins-agent:0.0.2
    command: ['sh', '-c', 'echo "Hello, Kubernetes!" && sleep 3600']
    volumeMounts:
    - name: kubeconfig
      mountPath: /mnt
      readOnly: true
    env:
    - name: KUBECONFIG
      value: /mnt/kubeconfig.yaml
  volumes:
  - name: kubeconfig
    secret:
      secretName: kubeconfig
  dnsPolicy: ClusterFirst
  restartPolicy: Always
'''
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

