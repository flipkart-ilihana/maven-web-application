node{

echo "Job Name is: ${env.JOB_NAME}"
echo "Node name is: ${env.NODE_NAME}"
 
 properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
 def mavenHome = tool name: 'mven3.8.4'

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
}
