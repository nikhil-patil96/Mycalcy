currentBuild.displayName = "Mycalcy-Test-#"+currentBuild.number


pipeline{
    agent any
    environment{
    PATH="/usr/share/maven:$PATH" //maven path
    }
    
    
 stages{
    stage("Git Checkout"){
        steps{
            git credentialsId: 'github', url: 'https://github.com/nikhil-patil96/Maven-Project/'
            // doing git checkout using credentials in jenkins with id "github" and repo url https://github.com/nikhil-patil96/Maven-Project
        }
    }
    stage("Maven Build"){
        steps{
            sh "mvn clean package" 
            sh "mv target/*.war target/myweb.war" //rename war file.
            
        }
    }
    stage("deploy-dev"){
             steps{
             sshagent(['tomcat-new']) {
              sh """
                scp -o StrictHostKeyChecking=no target/myweb.war ubuntu@172.31.13.127:/home/ubuntu/tomcat/webapps
                
                  ssh ubuntu@172.31.13.127 /home/ubuntu/tomcat/bin/shutdown.sh //stop tomcat
                
                 ssh ubuntu@172.31.13.127 /home/ubuntu/tomcat/bin/startup.sh //start tomcat
                
              """
             }
        }
    }
 }
 
}
