pipeline {
    agent none
    stages {
        stage('Build') {
            agent {
               docker {
                 image 'maven:3-alpine'
                 args '-v /root/.m2:/root/.m2'
            }
         }
         steps {
            sh 'mvn -B -DskipTests clean package'
         }
       }
       stage('Test') {
            steps {
                sh 'mvn test' 
            }
                 
        }
        stage('docker-build') {
           agent {
               label 'master'
           }
           steps {
              sh 'echo test'
           }
        }
      }
}
    
 
