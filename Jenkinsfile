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
                }
            }
       	    steps 
	    {
                sh 'mvn -B -DskipTests clean package'
	    }
	}
        stage('Test')
	{
	  agent {
		  image 'maven:3-alpine'
                    args '-v /root/.m2:/root/.m2'
		 reuseNode true
		}
		  
            steps
	    {
                 sh 'mvn test'
            }
         }
     }
 }
 
