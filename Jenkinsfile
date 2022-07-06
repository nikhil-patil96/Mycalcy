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
            sshPublisher(publishers: [sshPublisherDesc(configName: 'deploy tomcat', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/home/ubuntu/package', remoteDirectorySDF: false, removePrefix: 'target', sourceFiles: 'target/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: true)])
                 /*
            sshagent(['Tomcat']) {
            
                sh """
                scp -o StrictHostKeyChecking=no target/CalcyTest1.war ubuntu@13.127.243.181:/home/ubuntu/tomcat/webapps
                ssh ubuntu@13.127.243.181 /home/ubuntu/restart.sh
                """
            }*/
                 /*
             sshagent(['tomcat-new']) {
              sh """
                scp -o StrictHostKeyChecking=no target/CalcyTest1.war ubuntu@13.127.243.181:/home/ubuntu/tomcat/webapps
                
                  ssh ubuntu@13.127.243.181 /home/ubuntu/tomcat/bin/shutdown.sh //stop tomcat
                
                 ssh ubuntu@13.127.243.181 /home/ubuntu/tomcat/bin/startup.sh //start tomcat
                
              """
             }*/
        }
    }
 }
 
}
