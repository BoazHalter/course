pipeline 
{
  agent none 
  
  stages 
  { 
	stage('Run Compiler') 
	{
        agent 
		{
            docker 
			{
                image 'maven:3-alpine'
                args '-v /root/.m2:/root/.m2'	
            }
        }
	    stages 
		{
		    stage('Build')
			{
		        steps
		        {
                    sh 'mvn -B -DskipTests clean package'
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
	stage('docker-build')
	{
	    agent {label 'master'}
	    steps {
		    sh 'docker build . -t 10.0.0.26:5012/timetracker:${env.BUILD_NUMBER}'
	    }
	}
    }
}
