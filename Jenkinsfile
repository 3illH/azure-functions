def FAILED_STAGE
pipeline {
  agent any
  environment {
    MAVEN_OPTS = "-Dmaven.repo.local=/m2"
    DOCKERHUB_CREDENTIALS=credentials('dockerCredentials')
    ARGOCDIP=credentials('argocdip')
  }
  stages {
    stage('Checkout SMC') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: 'master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/3illH/azure-functions']]])
      }
    }
    stage('Build') {
      steps {
        echo 'Hello, Jenkins'
      }
    }
  }
}