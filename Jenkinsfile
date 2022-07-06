currentBuild.displayName = "Mycalcy-Test-#"+currentBuild.number


pipeline{
    agent any
    environment{
    PATH="/usr/share/maven:$PATH" //maven path
    }
    
    
 stages{
    stage("Git Checkout"){
        steps{
            git credentialsId: 'github', url: 'https://github.com/nikhil-patil96/Mycalcy.git/'
            // doing git checkout using credentials in jenkins with id "github" and repo url https://github.com/nikhil-patil96/Maven-Project
        }
    }
    stage("Maven Build"){
        steps{
            sh "mvn clean package" 
            sh "mv target/*.war target/CalcyTest1.war" //rename war file.
            
        }
    } 
    stage("deploy-dev"){
             steps{
             sshagent(['tomcat-new']) {
              sh """
                scp -o StrictHostKeyChecking=no target/CalcyTest1.war ubuntu@13.127.243.181:/home/ubuntu/tomcat/webapps
                
                  ssh ubuntu@13.127.243.181 /home/ubuntu/tomcat/bin/shutdown.sh //stop tomcat
                
                 ssh ubuntu@13.127.243.181 /home/ubuntu/tomcat/bin/startup.sh //start tomcat
                
              """
             }
        }
    }
 }
 
}
