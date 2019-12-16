@Library('my-shared-lib')_


node 
{
	def app
	try {
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
	catch(e) 
	{
		throw e
	}
	finally
	{
            slackNotifier(currentBuild.currentResult)
            cleanWs()
        }
    	
}


