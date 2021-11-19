pipeline {
  agent { label "master" }
  stages {
    stage("build") {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', passwordVariable: 'pass', usernameVariable: 'user')]) {
          // the code here can access $pass and $user
          sh """
          docker build -t myweb:5.0 .
          docker login -u $user -p $pass
          docker tag myweb:5.0 tranhuuhoa/myweb:5.0
          docker push tranhuuhoa/myweb:5.0
        """
       }
        
      }
    }
    stage("run") {
      steps {
        withKubeConfig([credentialsId: 'jenkins-robot-token', serverUrl: 'https://192.168.59.100:8443']) {
          sh 'kubectl create deployment myweb --image=tranhuuhoa/myweb:5.0'
        }
      }
    }
  }
}
