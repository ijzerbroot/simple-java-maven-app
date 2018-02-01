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
    stage('Build') {
      steps {
    //    container('maven') {
    //      git 'https://github.com/ijzerbroot/simple-java-maven-app'
    //    }
        container('maven') {
          sh 'mvn -B clean install'
        }
      }
    }
    stage('build & SonarQube Scan') {
    steps {
      withSonarQubeEnv('Sapienza Sonar') {
        container('maven') {
        sh 'mvn clean package sonar:sonar'
        }
      } // SonarQube taskId is automatically attached to the pipeline context
    }
  }


// No need to occupy a node
stage("Quality Gate") {
 timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
   def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
   if (qg.status != 'OK') {
     error "Pipeline aborted due to quality gate failure: ${qg.status}"
   }
 }
}

  }
}
