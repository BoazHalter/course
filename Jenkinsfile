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
    agent {
        master {
            stage('Build & Publish docker image') { 
            steps {
                sh 'docker build . -t 10.0.0.26:5012/java-with-time-tracker:${BUILD_NUMBER}' 
                }
            }
        }
    }
    
}
