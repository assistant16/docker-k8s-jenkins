pipeline {
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
    stage('Build Docker Image') {
      steps {
        container('docker') {  
          sh 'docker version'
          sh 'docker build -t test .'
          sh 'docker run -dp 8080:8080 test'
          sh 'sleep 100'
        }
      }
    }
  }
}
