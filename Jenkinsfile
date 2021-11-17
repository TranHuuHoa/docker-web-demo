pipeline {
  agent { label "master" }
  stages {
    stage("build") {
      steps {
        sh """
          docker build -t hoath/web:1.0 .
        """
      }
    }
    stage("run") {
      steps {
        sh """
          docker run --name hoath-web -p 8080:8080 -d hoath/web:1.0
        """
      }
    }
  }
}