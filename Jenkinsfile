def sendSlackNotifications(String buildStatus = 'STARTED') {
  
  buildStatus =  buildStatus ?: 'SUCCESS'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESS') {
    color = 'GREEN'
    colorCode = '#00FF00'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary)
}

node{

echo "Job Name is: ${env.JOB_NAME}"
echo "Node name is: ${env.NODE_NAME}"
 
 properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
 
 def mavenHome = tool name: 'mven3.8.4'

 try{
 }//Try closing
 }//Node Closing
 
//Get the code from Github Repo
stage('CheckoutCode'){
git branch: 'development', credentialsId: '30818f7a-8627-428d-9866-284af7661306', url: 'https://github.com/flipkart-ilihana/maven-web-application.git'
 }
//Do the build by using Maven Build tool
stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}
/*
//Execute the SonarQube Report 
stage('ExecuteSonarQubeReport'){
sh "${mavenHome}/bin/mvn sonar:sonar"
}

//Upload Artifacts into Artifactory Repo
stage('UploadArtifactsintoNexus'){
sh "${mavenHome}/bin/mvn deploy"
}

//Deploy Application into Tomcat Server
stage('DeployApplicationIntoTomcatServer'){
sshagent(['daa846c8-2937-4aed-ba09-8f348a09e47f']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@44.201.177.66:/opt/apache-tomcat-9.0.62/webapps/"
}

}
*/
}//Try Closing
  catch(e){
  currentBuild.result = "FAILED"
  }
  finally{
   
sendSlackNotifications(currentBuild.result) 
  }
}//Node Closing

