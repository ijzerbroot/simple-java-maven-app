podTemplate(cloud: 'kubernetes', label: 'maven', containers: [
 containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', ttyEnabled: true, command: 'cat')
 ],
  volumes: [
    hostPathVolume(mountPath: '/path/docker.sock', hostPath: '/path/docker.sock')
    // ,persistentVolumeClaim(mountPath: '/path/repository/', claimName: 'jenkins-maven-claim', readOnly: false)
  ]) {

  node('maven') {

    container('maven') {
      configFileProvider(
      [configFile(fileId: '<some-id>', variable: 'MAVEN_SETTINGS')]) {

        withMaven() {
            stage('Checkout') {
              checkout scm
            }

            stage('Build') {
              if (env.BRANCH_NAME == 'development') {
                sh "mvn -s '${MAVEN_SETTINGS}' clean deploy"
              } else {
                sh "mvn -s '${MAVEN_SETTINGS}' clean verify"
              }
            }

    //        stage('SonarQube') {
    //         sh "mvn -s '${MAVEN_SETTINGS}' sonar:sonar"
    //       }
        }
      }
    }

   // container('kubectl') {

    //  stage('Deployment') {
          // deploy on kubernetes
    //      ...
    //  }
    }

  }
}
