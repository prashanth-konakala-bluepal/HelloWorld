pipeline{		 
		 agent any
		 
		 environment
			 {
			  PATH = "/opt/apache-maven-3.6.3/bin:$PATH"
			 }
		 
			 {
			  PATH = "/opt/jdk-11.0.10/bin:$PATH"
			 }
		 stages
				{
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
									 sh "mv /var/lib/jenkins/workspace/sample_pipeline/webapp/target/*.war /var/lib/jenkins/workspace/sample_pipeline/webapp/target/simpleweb.war"
									}
							 } 
						stage('Deployment Selection')
							{
							 steps
									{
									script {
											CHOICES = ["Deploy to Dev", "Deploy to Test"];    
													env.YourTag = input  message: 'Where to Deploy.?', ok : 'Deploy', id :'tag_id',
																parameters:[choice(choices: CHOICES, description: 'Select a tag for this build', name: 'TAG')]
											}           
									echo "${env.YourTag}"
									}
							}				
						stage('Deploy to Dev')
									{
									 when
										{
										 expression { env.YourTag == 'Deploy to Dev' } 
										}
									 steps
											{
											 sshagent(['Tomcat'])
													{
													 sh """
													
														scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/sample_pipeline/webapp/target/simpleweb.war ubuntu@3.143.17.169:/opt/tomcat/webapps/
														
														ssh ubuntu@3.143.17.169 /opt/tomcat/bin/shutdown.sh
														
														ssh ubuntu@3.143.17.169 /opt/tomcat/bin/startup.sh
														
													"""
													}
											}
									}	
						stage('Deploy to Test')
									{
									 when
										{
										 expression { env.YourTag == 'Deploy to Test' }
										}
										 steps
												{
												 sshagent(['Tomcat-2'])
														{
														 sh """
													
															scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/sample_pipeline/webapp/target/simpleweb.war ubuntu@18.221.59.213:/opt/tomcat/webapps/
																
															ssh ubuntu@18.221.59.213 /opt/tomcat/bin/shutdown.sh
																
															ssh ubuntu@18.221.59.213 /opt/tomcat/bin/startup.sh
																
														"""
														}
												}
									}
				}
		}
