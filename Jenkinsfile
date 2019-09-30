pipeline{

agent any                                                                      

stages
{
	stage ('scm checkout')
{
git 'https://github.com/sopanjadhav07/maven-project.git'	
}
}

{
stage('code test') 
{

steps 
{
withAnt(ant: 'Local_Ant') 
{
     sh 'ant test'
}	 
}
}	
}

{
stage('code package') 
{

steps 
{
withAnt(ant: 'Local_Ant') 
{
     sh 'ant package'
}
}
} 
}


{
stage('code deploy') 
{

steps 
{
withAnt(ant: 'Local_Ant') 
{
     sh 'ant deploy'
}
}
}
}

{
stage ('SonarQube analysis')

steps {
     withSonarQubeEnv(sonar: 'sonar') {
	 sh 'ant install sonar:sonar'
    
}
}
}

{
stage ('deploy to tomcat'){

steps {
  sshagent (['172.31.39.232']) {
    sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@172.31.39.232:/var/lib/tomcat/webapps'
  }
}
}
}
}
