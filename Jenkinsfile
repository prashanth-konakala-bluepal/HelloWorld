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
					  }
				 }
			   }
		}
