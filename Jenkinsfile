pipeline {
  agent any
  stages {
    stage('Pull From Git') {
      steps {
        git(url: 'https://github.com/BoazHalter/course.git', branch: 'master', changelog: true, poll: true, credentialsId: 'BoazHalter:boaz286455')
      }
    }
     stage('Build') { 
            steps {
                sh 'printenv'
               //sh 'mvn package'  
               //sh 'mvn -B -DskipTests clean package' 
            }
     }
  }
}
