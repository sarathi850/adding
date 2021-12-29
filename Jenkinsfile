pipeline{
    agent any
    
    environment{
        PATH = "/opt/apache-maven-3.8.4/bin:$PATH"
    }
    stages{
        stage("Git Checkout"){
            steps{
                git branch: 'main', url: 'https://github.com/sarathi850/adding.git'
            }
        }
        stage("Maven Build"){
            steps{
                sh "mvn clean package"
                sh "mv target/*.war target/myweb.war"
            }
        }
        stage("deploy-dev"){
            steps{
                sshagent(['tomcat-new']) {
                sh """
                    mv -o StrictHostKeyChecking=no target/myweb.war  centos@13.235.254.20:/opt/tomcat/apache-tomcat-9.0.56/webapps/
                    
                    ssh centos@13.235.254.20 /opt/tomcat/apache-tomcat-9.0.56/bin/shutdown.sh
                    
                    ssh centos@13.235.254.20 /opt/tomcat/apache-tomcat-9.0.56/bin/startup.sh
                
                """
            }
            
            }
        }
    }
}
     
