pipeline {
  agent { label "master" }
  stages {
    stage("build") {
      steps {
        sh """
          docker build -t myweb:4.0 .
        """
      }
    }
    stage("run") {
      steps {
        sh """
          kubectl create deployment myweb --image=myweb:4.0
        """
      }
    }
  }
}
