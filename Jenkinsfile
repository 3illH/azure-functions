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
    // stage('Setup .NET') {
    //   steps {
    //     sh 'apt-get install -y dotnet-sdk-6.0'
    //   }
    // }
    stage('Restore') {
      steps {
        echo 'Hello, Jenkins'
        sh 'ls -lrt'
        sh 'dotnet restore azure-functions.csproj'
        // dotnetRestore project: 'azure-functions.csproj', sdk: 'net6'
        // dotnetBuild project: 'azure-functions.csproj', sdk: 'net6'
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