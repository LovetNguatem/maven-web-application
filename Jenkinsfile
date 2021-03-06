
//Jenkins Pipeline script 
//Groovy 


node
	{ 
def mavenHome = tool name: 'Maven3.6.3'

stage ('1. code clone')
	{
git credentialsId: 'GitHub_credentials', url: 'https://github.com/LovetNguatem/maven-web-application.git'

}

stage ('2. CodeBuild')
	{
sh "${mavenHome}/bin/mvn package"

}

stage ('3. CodeQuality')
	{

sh "${mavenHome}/bin/mvn sonar:sonar"


}
stage ('4. ArtifactRepo')
	{

sh "${mavenHome}/bin/mvn deploy"

}
 
stage ('5. Approval')
	{
echo "Approved. Ready for deployment"

}

stage ('6. DeployTomcat')
	{

deploy adapters: [tomcat9(credentialsId: 'tomcat_credentials', path: '', url: 'http://3.82.202.35:8080')], contextPath: null, war: 'target/*war'
}

stage ('7. EmailNotification')
	{
emailextrecipients([developers()])

}

}
