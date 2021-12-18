node
{
    def mavenHome=tool name: "maven3.8.3"
    
    stage('Checkout')
  {  
     git branch: 'development', credentialsId: 'd239ee77-52c1-4671-8079-94c19d5c7500', url: 'https://github.com/neerajdevops999/maven-web-application.git'
  } 
 
   stage('Build')
  {
    sh "${mavenHome}/bin/mvn clean package"
  } 
  
   stage ('ExecuteSonarQubeReport')
  {
    sh "${mavenHome}/bin/mvn sonar:sonar"
  }
  
   stage ('UploadArtifactIntoNexus')
  {
    sh "${mavenHome}/bin/mvn deploy"
  }
  
   stage('DeployAppIntoTomcat')
  {
    sshagent(['5d792433-e511-4f5c-a82f-8a9cd1d383a3'])
  {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.126.173.214:/opt/apache-tomcat-9.0.54/webapps/"
  }
  }
  
  satge('SendEmailNotification')
 {
    mail bcc: '', body: '''Build Over 

    Regars
    Neeraj Jr Devops Enginner''', cc: 'k08pradeep@gmail.com', from: '', replyTo: '', subject: 'Build Over', to: 'neerajsai316@gmail.com'
 }
 
}
