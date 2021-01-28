node ( 'master' )
{
def mavenHome = tool name: "maven3.6.3"
stage( 'CcheckoutCode' )
{
git branch: 'development', credentialsId: '48f09e28-d1a5-4467-b9e3-679491d03d7c', url: 'https://github.com/ashish-8/maven-web-application.git'
}
stage( 'Build' )
{
sh "${mavenHome}/bin/mvn clean package"
}
stage( 'Excute SoanrQube Report' )
{
sh "${mavenHome}/bin/mvn sonar:sonar"
}
stage ( 'Upload Artifact into Nexus' )
{
sh "${mavenHome}/bin/mvn deploy"
}
stage ( 'Deploy application to Tomcatsever' )
{
sshagent(['4ca13a74-a169-47fe-b576-1d08be38c556']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.235.94.246:/opt/apache-tomcat-9.0.41/webapps/"
}
}
stage ('Email notification' )
{
mail bcc: '', body: '''Bulid over

Regards,
Ashish Dwivedi''', cc: 'ashishdwivedi457@gmail.com', from: '', replyTo: '', subject: 'Build over..', to: 'ashishdwivedi457@gmail.com'
}
}
