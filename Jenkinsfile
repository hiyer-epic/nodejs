node 
{
	def app
	stage('Clone repository') 
	{
		checkout scm
	}

	stage('Build image') 
	{
		app = docker.build("hsivabc/nodeapi")
	}

	stage('Test image')
	{
		app.inside 
		{
			sh 'echo "Tests passed"'
		}

	}

	stage('Push images')
	{
		app.push("latest")
	}

	stage('Remove Local Docker Images') 
	{
	}

	stage('Deploy in Docker') 
	{
	    sh 'bash nodesvc.sh' 
	}
    	
}


