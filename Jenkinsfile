pipeline {
  agent {
    kubernetes {
      //cloud 'kubernetes'
      label 'maven'
      containerTemplate {
        name 'maven'
        image 'maven:3.3.9-jdk-8-alpine'
        ttyEnabled true
        command 'cat'
      }
    }
  }
  stages {
   stage('Get the code') {
    git 'https://github.com/ijzerbroot/simple-java-maven-app'
   }
    stage('Run maven') {
      steps {
        container('maven') {
          sh 'mvn -B clean install'
        }
      }
    }
  }
}

