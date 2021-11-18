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
          docker run --name myweb -p 8081:8080 -d myweb:4.0
        """
      }
    }
  }
}
