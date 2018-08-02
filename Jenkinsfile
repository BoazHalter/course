pipeline 
{
	
  agent none 
  withEnv([]) {
    deploy = true
}

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
			  sh '''mvn sonar:sonar \
  				-Dsonar.organization=boazhalter-github \
  				-Dsonar.host.url=https://sonarcloud.io \
  				-Dsonar.login=31fefaf1f833f46277297fcde612b9fdeb6f9cbe''' 
                         
				
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
  }
}
node{
	env.REGISTRY = '10.0.0.26:5012'
	env.PORT=8082
	
	stage('docker-build') {
	   sh '''
	         set -e
	         docker rmi -f $(docker images  | grep "timetracker"|awk '{print $3}')
	         docker rm -f $( docker ps -a  |grep 'timetracker'|awk '{print $1}')'''
	   //sh 'docker build -t timeframes:1.0 .'
	   sh 'docker tag timeframes:1.0 ${REGISTRY}/timetracker:1.0.${BUILD_ID}'
	}
	stage('publish artifacts'){
	   sh ' docker push ${REGISTRY}/timetracker:1.0.${BUILD_ID}'
	  }
	if ( deploy ) {
    	stage('Deployment')
	{ 
		
		sh 'docker run --name-d -p ${PORT}:8080 ${REGISTRY}/timetracker:1.0.${BUILD_ID}'
		echo 'http://10.0.0.26:${PORT}/time-tracker-web-0.3.1/'
		
	}
    }

}
	
