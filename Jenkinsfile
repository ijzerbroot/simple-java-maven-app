podTemplate(label: 'maven', containers: [
 containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', ttyEnabled: true, command: 'cat')
 ]
            //,
  //volumes: [
  //  hostPathVolume(mountPath: '/path/docker.sock', hostPath: '/path/docker.sock')
    // ,persistentVolumeClaim(mountPath: '/path/repository/', claimName: 'jenkins-maven-claim', readOnly: false)
  //]
           ) {

      node('maven') {
        stage('Get a Maven project') {
      //      git 'https://github.com/jenkinsci/kubernetes-plugin.git'
            container('maven') {
                stage('Build a Maven project') {
                    sh 'mvn -B clean install'
                }
            }
        }

  }
}
