pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps { git 'https://github.com/your-username/my-devops-app.git' }
    }
    stage('Build Docker Image') {
      steps { sh 'docker build -t your-dockerhub-user/my-devops-app:latest .' }
    }
    stage('Push to DockerHub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
          sh 'echo $PASS | docker login -u $USER --password-stdin'
          sh 'docker push your-dockerhub-user/my-devops-app:latest'
        }
      }
    }
    stage('Deploy to Kubernetes') {
      steps { sh 'kubectl apply -f k8s/deployment.yaml' }
    }
  }
}
