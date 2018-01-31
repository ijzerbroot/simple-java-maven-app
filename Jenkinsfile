pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -V -U -e clean package'
      }
    }
  }
}