pipeline {
		  agent any
		  environment
					 {
					  PATH = "/opt/apache-maven-3.6.3/bin:$PATH"
					 }
		  stages
				{
				 stage("clone code")
					{
					 steps
						  {
						   echo 'Cloneing Done'
						  }
					}
				stage("build code")
					{
					 steps
						  {
						   sh "mvn clean install"
						  }
					}
				stage("deploy")
					{
					 steps
						  {
						   sshagent(['deploy_root']) 
						   {
						   sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war root@3.16.137.122:/opt/tomcat/webapps"
						   }
						  }
					}
				}
		 }
