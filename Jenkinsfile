pipeline {
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /root/.m2:/root/.m2'
    }

  }
  stages {
    stage('Pull From Git') {
      steps {
        git(url: 'https://github.com/BoazHalter/course.git', branch: 'master', changelog: true, poll: true, credentialsId: 'BoazHalter:boaz286455')
      }
    }
    stage('Build') {
      steps {
        sh 'printenv'
      }
    }
  }
}