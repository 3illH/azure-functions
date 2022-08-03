def FAILED_STAGE
pipeline {
  agent any
  environment {
    MAVEN_OPTS = "-Dmaven.repo.local=/m2"
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
        sh 'ls -lrt'
        dotnetRestore project: '*.csproj', sdk: 'net6'
      }
    }
  }
  post {
      // Clean after build
      always {
          cleanWs(cleanWhenNotBuilt: false,
                  deleteDirs: true,
                  disableDeferredWipeout: true,
                  notFailBuild: true,
                  patterns: [[pattern: '.gitignore', type: 'INCLUDE'],
                             [pattern: '.propsfile', type: 'EXCLUDE']])
      }
  }
}