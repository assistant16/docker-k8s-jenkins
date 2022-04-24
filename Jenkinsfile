pipeline {
  environment {
    dockerhub=credentials('dockerhub')
  }
  agent any
    stage('build Docker image') {
      agent {
        kubernetes {
          yamlFile 'docker-pod.yaml'
        }
      }
      steps {
        container('docker') {  
          sh 'docker build -t docker-k8s-jenkins .'
          sh 'docker tag docker-k8s-jenkins assistant16/docker-k8s-jenkins:latest '
          sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin'
          sh 'docker push assistant16/docker-k8s-jenkins:latest'
        }
      }
    }
    stage('Kubectl apply changes') {
      agent any
        steps {
          withKubeConfig([credentialsId: 'secretfile']) {
            sh 'curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.20.5/bin/linux/amd64/kubectl"'  
            sh 'chmod u+x ./kubectl'  
            sh './kubectl get nodes'
            sh './kubectl apply -f deployment.yaml'
            sh './kubectl apply -f service.yaml'
          }
        }
      }
   }
}
