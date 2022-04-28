node{
    def mavenHome = tool name: "maven 3.8.5"
   echo "The Buid num is: ${BUILD_NUMBER}"
   echo "The Build ID : ${BUILD_ID}"
   echo "The job namE : ${JOB_NAME}"
    
    echo 'THIS IS SCRIPTED WAT PROJECT'
    
    properties([pipelineTriggers([cron('3 11 28 4 4')])])
    pwd()
    stage('checkout'){
      git branch: 'development', credentialsId: '712de447-e509-47f1-9bb3-827aa8bedb07', url: 'https://github.com/mss-devops-janbatch-6/maven-web-application.git'  
    }
    //Build stage
    stage('Build'){ 
        sh "$mavenHome/bin/mvn clean package"
    }
    //Generate Sonarqube Report
    stage('sonarqube report'){
        sh "$mavenHome/bin/mvn sonar:sonar"
    }
    //Upload package into Artifact Repository
    stage('Artifact Repository'){
        sh "$mavenHome/bin/mvn deploy"
    }
    //Tomcat
    stage('Tomcat'){
       sshagent(['ebae3f3b-63d9-4799-a06d-fe703c96697c']) {
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.84.43:/opt/apache-tomcat-9.0.59/webapps"
    }
    }
    
}//node closing
