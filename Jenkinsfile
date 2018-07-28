pipeline {
  agent {
    docker {
      args 'mvn -B -DskipTests clean package'
      image 'maven:3-alpine'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
  }
}