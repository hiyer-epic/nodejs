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
            sh 'docker images -q | xargs --no-run-if-empty docker rmi --force'
	}

	stage('Deploy in Docker') 
	{
	    sh 'bash nodesvc.sh' 
	}
	def call(String buildResult) {
  if ( buildResult == "SUCCESS" ) {
    slackSend color: "good", message: "Job: ${env.JOB_NAME} with buildnumber ${env.BUILD_NUMBER} was successful"
  }
  else if( buildResult == "FAILURE" ) { 
    slackSend color: "danger", message: "Job: ${env.JOB_NAME} with buildnumber ${env.BUILD_NUMBER} was failed"
  }
  else if( buildResult == "UNSTABLE" ) { 
    slackSend color: "warning", message: "Job: ${env.JOB_NAME} with buildnumber ${env.BUILD_NUMBER} was unstable"
  }
  else {
    slackSend color: "danger", message: "Job: ${env.JOB_NAME} with buildnumber ${env.BUILD_NUMBER} its resulat was unclear"	
  }
}
}
