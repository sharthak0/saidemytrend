pipeline { 
    agent  any  
    environment { 
       	PATH = "/opt/maven/bin:$PATH" 
      } 
    stages { 
       stage('bulding') { 
         steps { 
            sh 'mvn clean deploy'  
          }  
       }  
         stage('sonarqube analysis') { 
            environment { 
             scannerHome = tool 'my-sonar-scanner'  
            } 
            steps{ 
              withSonarQubeEnv('my-sonarqube-server') {
 
                sh "$(scannerHome)/bin/sonar-scanner"

               }            
             } 
           } 
       } 
  }      
               

