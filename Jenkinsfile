node
{

	def mvnHome= tool name:'maven3.6.1', type: 'maven'

stage('checkoutcode')
{
	git branch: 'development', credentialsId: 'ad1aa34b-7135-4b90-b980-f1388467cb4e', url: 'https://github.com/shivakugunavar/maven-web-application.git'
}

stage('Build')
{
	if(isUnix())
	{
		sh "${mvnHome}/bin/mvn clean deploy sonar:sonar"
	}	
}

stage('DeployTomcat')
{
	sshagent(['keyid'])
 	{
		sh "scp -o StrictHostkeyChecking=no  target/*.war ec2-user@13.232.182.92:/opt/apache-tomcat-9.0.22/webapps/"
		
	}
}
}
