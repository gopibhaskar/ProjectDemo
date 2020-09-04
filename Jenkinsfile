  /* This script will provide basic idea to create jenkins file and deploy application on deployment environment.
Deployment environment can be anything like Docker, kubernetes or cloud.
Create 'deploy.properties' file at same location and save all the build and deployment properties. This file will be refered by this pipeline for build and deployment. */
def workspace;
def props='';
def tagName="""${JOB_NAME}-${BUILD_TIMESTAMP}"""
def branchName;
def commit_username;
def commit_Email;
def appDeployProcess;
def imageName;
def envMessage='';
node{
    stage('Checkout Code')
    {
        try
        {
            checkout scm
     //       props = readProperties  file: """deploy.properties"""
			workspace = pwd ()
			/*branchName=sh(returnStdout: true, script: 'git symbolic-ref --short HEAD').trim()
			commit_username=sh(returnStdout: true, script: '''username=$(git log -1 --pretty=%ae)
																echo ${username%@*} ''').trim();
			commit_Email=sh(returnStdout: true, script: '''Email=$(git log -1 --pretty=%ae)
																echo $Email''').trim(); */
			branchName= "master"
			commit_username="Papanaboina, Gopibhaskar"
			commit_Email="Gopibhaskar.Papanaboina@sabre.com"
			echo commit_username
			echo commit_Email
			echo branchName
        }
    	catch (e) {
    		currentBuild.result='FAILURE'
    		//notifyBuild(currentBuild.result, "At Stage Checkout Code", "", commit_Email)
    		throw e
    	}
		catch (error) {
				currentBuild.result='FAILURE'
				//notifyBuild(currentBuild.result, "At Stage Checkout Code", "", commit_Email)
				throw error
			}
    }
	stage ('Check Environment')
    { 
    	try
		{
			//check if deployment environment is up and running
		}
	 catch (e) {
    		currentBuild.result='FAILURE'
    		//notifyBuild(currentBuild.result, "At Stage Check Environment", "", commit_Email)
    		throw e
    	}
    }
   /* stage ('Static Code Analysis')
    { 
     try{
			//sh """echo ${workspace}"""
			def scannerHome = tool 'sonar-runner';
			withSonarQubeEnv('SonarQContainer')
			{
				sh 'mvn clean package sonar:sonar'
			}
        }
    	catch (e) {
    		currentBuild.result='FAILURE'
    		//logJIRATicket(currentBuild.result,  "At Stage Static Code Analysis", props['JIRAprojectid'], props['JIRAissuetype'], commit_Email, props['JIRAissuereporter'])
    		//notifyBuild(currentBuild.result, "At Stage Static Code Analysis", "", commit_Email)
    		throw e
    	}
     }*/
    stage ('Build')
    { 
		try
		{
      		workspace = pwd ()
			sh """mvn clean compile package"""      
		}
		catch (e) 
		{
    		currentBuild.result='FAILURE'
    		//logJIRATicket(currentBuild.result,  "At Stage Build", props['JIRAprojectid'], props['JIRAissuetype'], commit_Email, props['JIRAissuereporter'])
    		//notifyBuild(currentBuild.result, "At Stage Build", "", commit_Email)
    		throw e
    	}
	 
    }
