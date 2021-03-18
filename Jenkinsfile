pipeline{
		 agent any
		 
		 environment
		 {
		  PATH = "/opt/apache-maven-3.6.3/bin:$PATH"
		 }
		 
		 stages{
			    stage("Git Checkout")
					{
					 steps
						  {
						   git branch: 'main', url: 'https://github.com/prashanth-konakala-bluepal/HelloWorld.git'
						  }
					}
			     stage("Maven Build")
				 {
				  steps
					  {
					   sh "mvn clean package"
					   // sh "mv /var/lib/jenkins/workspace/sample_pipeline/webapp/target/*.war target/myweb.war"
					  }
				 }
				 stage("Deploy-dev")
				 {
				  steps
						{
						 sshagent(['Tomcat'])
							{
								sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@172.31.9.46:/opt/tomcat/webapps/'
								sh 'ssh ubuntu@172.31.9.46 /opt/tomcat/bin/shutdown.sh'
								sh 'ssh ubuntu@172.31.9.46 /opt/tomcat/bin/startup.sh'
							}
						}
				 }
			   }
		}
