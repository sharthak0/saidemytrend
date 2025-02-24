
pipeline {
    agent any 
    environment { 
      PATH = "/opt/maven/bin:$PATH"  
   }
stages{ 
   stage('build') { 
      steps{ 
         sh 'mvn clean deploy' 
      }
    }   
    
    stage('sonarqube analysis'){ 
       environent{  
          scannerHome = Tool 'my-sonar-scanner' 
       }
    steps{ 
          withsonarqubeenv (my-sonarqube-server) { 
     

              sh "${scannerHome}/bin-sonar-sanner" 
          } 
        }
     
    } 
  } 
} 

