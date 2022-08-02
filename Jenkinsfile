def FAILED_STAGE
pipeline {
  agent {
    kubernetes {
      yamlFile 'build-pod.yaml'
    }

  }
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
        container('maven') {
          script {
            pom = readMavenPom file: "pom.xml";
            sh "mvn clean package -DskipTests"
          }
        }
      }
    }
}