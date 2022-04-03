node{
def mavenHome = tool name: "maven3.8.5"
//Checkout statge
stage('CheckoutCode'){
git branch: 'development', credentialsId: 'd0b1abf3-bf65-4c65-8ab4-26798dffc91b', url: 'https://github.com/mss-devops-janbatch-6/maven-web-application.git'
}
//Build stage
stage('Build'){
sh "$mavenHome/bin/mvn clean package"
}
//Generate SonarQube Report
stage('sonarqube report'){
sh "$mavenHome/bin/mvn sonar:sonar"
}
//Upload Artifact into Artifcatory repo
stage('Artifact'){
sh "$mavenHome/bin/mvn deploy"
}
//Deploy App into Tomcat Server
stage('DeployAppIntoTomcat'){
sshagent(['e6afd867-be34-4f54-8a40-4840ac85faa0']) {
 sh "scp -o StrictHostKeyChecking=no target/maven-web-application.warec2-user@13.127.219.175:/opt/apache-tomcat-9.0.59/webapps"
}
}
}// Node closing
