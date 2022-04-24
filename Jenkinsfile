pipeline {
  agent any
  stages {
    stage('Build') {
     agent {
      kubernetes {
      yamlFile 'docker-pod.yaml'  // path to the pod definition relative to the root of our project
     }
    }
      steps {  
        sh "ls"  
        sh "docker -versions"
      }
    }
      stage('List NODES') {
           steps {
               withKubeConfig([credentialsId: 'secretfile']) {
                sh 'curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.20.5/bin/linux/amd64/kubectl"'  
                sh 'chmod u+x ./kubectl'  
                sh './kubectl get nodes'
               }
          }
      }
   }
}
