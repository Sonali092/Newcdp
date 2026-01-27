pipeline {
  agent any

  environment {
    IMAGE_NAME = "custom-nginx"
    IMAGE_TAG  = "${BUILD_NUMBER}"
  }

  stages {

    stage('Clone Repository') {
      steps {
        git branch: 'main',
            url: 'https://github.com/Sonali092/Newcdp.git'
      }
    }

    stage('Build NGINX Docker Image') {
      steps {
        sh '''
          echo "Building image: ${IMAGE_NAME}:${IMAGE_TAG}"
          docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
        '''
      }
    }

    stage('Verify Image') {
      steps {
        sh 'docker images | grep ${IMAGE_NAME}'
      }
    }
  }

  post {
    success {
      echo "✅ Image built successfully: ${IMAGE_NAME}:${IMAGE_TAG}"
    }
  }
}
