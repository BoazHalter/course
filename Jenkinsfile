pipeline 
{
	environment { 
        REGISTRY = '10.0.0.26:5012'
    }
	
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
			  // sh '''mvn sonar:sonar \
  			//	-Dsonar.organization=boazhalter-github \
  			//	-Dsonar.host.url=https://sonarcloud.io \
  			//	-Dsonar.login=31fefaf1f833f46277297fcde612b9fdeb6f9cbe''' 
                         // sh 'mvn -B -DskipTests clean package'
				echo 'bal'
	                }
		    }
	       	stage('Test') 
			{		  
                steps
	            {
                //    sh 'mvn test'
			    echo 'bal'
                }
            }
        }	
        		
    }
  }
}
node{
	stage('docker-build')
	{
	
	    steps {
		
		    
		    sh 'docker build -t timeframes:1.0 .'
		    sh 'docker tag timeframes:1.0 ${REGISTRY}/timetracker:1.0.${BUILD_ID}'
		    
		    
	    }
	}
	stage('publish artifacts'){
		  steps{
			  sh ' docker push ${REGISTRY}/timetracker:1.0.${BUILD_ID}'
		  }
	  }
	

}
	
