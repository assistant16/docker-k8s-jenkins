pipeline {
  environment {
    dockerhub=credentials('dockerhub')
  }
  agent any
  stages {
    stage('Build') {
      steps {  // no container directive is needed as the maven container is the default
        sh "ls"   
        sh "git clone https://github.com/assistant16/docker-k8s-jenkins.git" 
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
               withKubeConfig([credentialsId: 'secretfile']) {
                sh 'kubectl get nodes'
                 }
                 }
      }
   }
}
