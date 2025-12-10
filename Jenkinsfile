pipeline {
  agent any

  options {
    timestamps()
    disableConcurrentBuilds()
  }

  environment {
      IMAGE_NAME = "pankaj8900/springboot-app"
      TAG = "${BUILD_NUMBER}-${GIT_COMMIT.substring(0,7)}"
  }

  stages {

    stage('Checkout Code') {
      steps {
        git branch: 'main',
            url: 'https://github.com/codiebyheaart/Spring-Boot-MySQL-Deployment-on-Azure-Kubernetes-Service.git'
      }
    }

    stage('Build & Test') {
      steps {
        sh 'chmod +x gradlew'
        sh './gradlew clean build'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh "docker build -t $IMAGE_NAME:$TAG ."
      }
    }

    stage('Push to DockerHub') {
      steps {
        withCredentials([usernamePassword(
            credentialsId: 'dockerhub',
            usernameVariable: 'DOCKER_USER',
            passwordVariable: 'DOCKER_PASS'
        )]) {
            sh "docker login -u $DOCKER_USER -p $DOCKER_PASS"
            sh "docker push $IMAGE_NAME:$TAG"
        }
      }
    }

    stage('Archive Artifacts') {
      steps {
        archiveArtifacts artifacts: '**/*.jar'
      }
    }
  }

  post {
    success { echo "Build SUCCESS - Docker Image pushed!" }
    failure { echo "Build FAILED - Check Jenkins logs" }
  }
}
