pipeline {
    agent none
    stages { 
        
	stage('Build') 		
	{
            agent
	    {
                docker 
		{
                    image 'maven:3-alpine'
                    args '-v /root/.m2:/root/.m2'
		    reuseNode true	
                }
            }
       	    steps 
	    {
                sh 'mvn -B -DskipTests clean package'
	    }
	    stages {
               stage('In Sequential 1') {
                   steps {
                       echo "In Sequential 1"
                   }
               }
               stage('In Sequential 2') {
                   steps {
                       echo "In Sequential 2"
                   }
               }
            }
	}
        stage('Test')
	{		  
            steps
	    {
                 sh 'mvn test'
            }
         }
     }
 }
 
