pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test' 
            }
                 
        }
    }
    stages {      
        stage('boom'){
            steps { 
                node('master') {
                   sh'echo test'
                }
            }
        }
    }
}
    
 
