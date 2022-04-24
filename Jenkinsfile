pipeline {
  environment {
    dockerhub=credentials('dockerhub')
  }
  agent {
    kubernetes {
      yamlFile 'docker-pod.yaml'  // path to the pod definition relative to the root of our project
    }
  }
  stages {
    stage('Build') {
      steps {  // no container directive is needed as the maven container is the default
        sh "ls"   
        sh "git clone https://github.com/assistant16/docker-k8s-jenkins.git" 
      }
    }
  //  stage('Build Docker Image') {
   //   steps {
    //    container('docker') {  
     //     sh 'docker build -t docker-k8s-jenkins .'
     //   }
     // }
    //}
      stage('List NODES') {
           steps {
             container('curl') { 
               withKubeConfig([credentialsId: 'secretfile']) {
                sh 'curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.20.5/bin/linux/amd64/kubectl"'
                sh 'chmod u+x ./kubectl' 
                sh 'kubectl get nodes'
               }
             }
           }
       }
  }
}
