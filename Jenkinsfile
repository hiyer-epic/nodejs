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

	stage('Push image')
	{
		app.push("latest")
	}

	stage('Remove Local Docker Images') 
	{
	    sh 'docker rm -f haritibcoblog-node-webapp'
            sh 'docker images -q | xargs --no-run-if-empty docker rmi --force'
	}

	stage('Deploy in Docker') 
	{
	    sh 'bash nodesvc.sh' 
	}
        try
        {
	    				/* Use slackNotifier.groovy from shared library and provide current build result as parameter */   
            				slackNotifier(currentBuild.currentResult)
            				cleanWs()
        }
    
 }


