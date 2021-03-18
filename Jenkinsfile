pipeline{
		 agent any
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
				  step
					  {
					   sh "mvn clean package"
					  }
				 }
			   }
		}
