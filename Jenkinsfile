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
			steps
			{
				docker.withRegistry('http://10.0.0.26:5012') {
				def customImage = docker.build("my-image:${env.BUILD_ID}")
        			/* Push the container to the custom Registry */
        			customImage.push()
				sh 'docker ps'
				//sh 'docker build . -t 
				//def customImage = docker.build("my-image:${env.BUILD_ID}")
    				//customImage.push()
				}
			}
		}
}
}
