pipeline {
  agent { label "master" }
  stages {
    stage("build") {
      steps {
        sh """
          docker build -t myweb:4.0 .
          docker login -u tranhuuhoa -p
          docker tag myweb:1.0 tranhuuhoa/myweb:4.0
          docker push tranhuuhoa/myweb:4.0
        """
      }
    }
    stage("run") {
      steps {
        withKubeConfig([credentialsId: 'jenkins-robot-token', serverUrl: 'https://192.168.59.100:8443']) {
          sh 'kubectl create deployment myweb --image=tranhuuhoa/myweb:4.0'
        }
      }
    }
  }
}
