pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/nagendar47-hash/khaathwik.git'
      }
    }
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t nagendar47-hash/khaathwik:latest .'
      }
    }
    stage('Push to DockerHub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'khaathwik', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
          sh 'echo $PASS | docker login -u $USER --password-stdin'
          sh 'docker push nagendar47-hash/khaathwik:latest'
        }
      }
    }
    stage('Deploy to Kubernetes') {
      steps {
        sh 'kubectl apply -f k8s/deployment.yaml'
      }
    }
  }
}
