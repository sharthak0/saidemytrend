pipeline { 
    agent  any  
    environment { 
       	PATH = "/opt/maven/bin:$PATH" 
      } 
    stages { 
       stage('bulding') { 
         steps {   
             echo "----------start building--------"
            sh 'mvn clean deploy -Dmaven.test.skip=true'   
             echo "---------stop buildin-----------"
          }  
       }    
        stage('testing') {  
            echo "------unti test start--------" 
            sh 'mvn surefire-report:report' 
            echo "------unit test stop---------"
            
         stage('sonarqube analysis') { 
            environment { 
             scannerHome = tool 'my-sonar-scanner'  
            } 
            steps{ 
              withSonarQubeEnv('my-sonarqube-server') {
 
                sh "${scannerHome}/bin/sonar-scanner"

               }            
             } 
           } 
       } 
  }      
               

