pipeline {
  agent any
  environment {
    DOCKERHUB_USER = 'YOUR_DOCKERHUB_USERNAME'
    IMAGE_NAME = 'cloudcart'
    CONTAINER_NAME = 'cloudcart'
    HOST_PORT = '8081'
  }
  stages {
    stage('Checkout') { steps { checkout scm } }
    stage('Build') {
      steps {
        sh 'docker build -t $DOCKERHUB_USER/$IMAGE_NAME:$BUILD_NUMBER .'
        sh 'docker tag $DOCKERHUB_USER/$IMAGE_NAME:$BUILD_NUMBER $DOCKERHUB_USER/$IMAGE_NAME:latest'
      }
    }
    stage('Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DH_USER', passwordVariable: 'DH_TOKEN')]) {
          sh 'echo "$DH_TOKEN" | docker login -u "$DH_USER" --password-stdin'
          sh 'docker push "$DOCKERHUB_USER/$IMAGE_NAME:$BUILD_NUMBER"'
          sh 'docker push "$DOCKERHUB_USER/$IMAGE_NAME:latest"'
          sh 'docker logout'
        }
      }
    }
    stage('Deploy on Jenkins EC2') {
      steps {
        sh 'docker pull "$DOCKERHUB_USER/$IMAGE_NAME:latest"'
        sh 'docker rm -f "$CONTAINER_NAME" || true'
        sh 'docker run -d --restart unless-stopped --name "$CONTAINER_NAME" -p "$HOST_PORT:80" "$DOCKERHUB_USER/$IMAGE_NAME:latest"'
      }
    }
  }
}
