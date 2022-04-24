pipeline {
  agent any
  stages {
    stage('Build') {
      steps {  
        sh "ls"   
        sh "git clone https://github.com/assistant16/docker-k8s-jenkins.git" 
      }
    }
      stage('List NODES') {
           steps {
               withKubeConfig([credentialsId: 'secretfile']) {
                sh 'kubectl get nodes' }
                 }
      }
   }
}
