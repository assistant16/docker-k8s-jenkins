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
    stage('Build Docker Image') {
      steps {
        container('docker') {  
          sh 'docker build -t docker-k8s-jenkins .'
          sh 'docker tag docker-k8s-jenkins assistant16/docker-k8s-jenkins:latest '
          sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin'
          sh 'docker push assistant16/docker-k8s-jenkins:latest
        }
      }
    }
  }
}
