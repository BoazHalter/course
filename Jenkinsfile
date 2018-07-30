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
		    sh 'curl -v -u admin:admin123 --upload-file /var/jenkins_home/workspace/pip/web/target/time-tracker-web-0.3.1.war http://10.0.0.26:8081/repository/maven-releases/org/timetracker/1.0/timetracker1.0.war'
		    sh 'docker build -t timetracker:1.0 .'
		    sh 'docker run -d -p 8888:8080 timetracker:1.0' 
		    
	    }
	}
    }
}
