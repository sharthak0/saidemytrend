#pipeline { 
    #agent  any  
    #environment { 
      # 	PATH = "/opt/maven/bin:$PATH" 
     # } 
    #stages { 
       #stage('bulding') { 
         #steps {   
           #  echo "----------start building--------"
          #  sh 'mvn clean deploy -Dmaven.test.skip=true'   
         #    echo "---------stop buildin-----------"
        #  }  
       #}    
        #stage('testing') {   
            #steps{
             #  echo "------unti test start--------" 
            #    sh 'mvn surefire-report:report' 
           #     echo "------unit test stop---------" 
          #  } 
        #}   
       #  stage('sonarqube analysis') { 
      #      environment { 
     #        scannerHome = tool 'my-sonar-scanner'  
    #        } 
   #         steps{ 
  #            withSonarQubeEnv('my-sonarqube-server') {
 #
 #               sh "${scannerHome}/bin/sonar-scanner"
#
     #          }            
    #         } 
   #        } 
  #     } 
 # }   

pipeline { 
    agent any  
    environment { 
        PATH = "/opt/maven/bin:$PATH" 
    } 
    stages { 
        stage('Building') { 
            steps {   
                echo "----------Start Building--------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'   
                echo "---------Stop Building-----------"
            }  
        }    

        stage('Testing') {   
            steps {
                echo "------Unit Test Start--------" 
                sh 'mvn surefire-report:report' 
                echo "------Unit Test Stop---------" 
            } 
        }   

        stage('SonarQube Analysis') { 
            steps { 
                script {
                    env.scannerHome = tool 'my-sonar-scanner'  
                }
                withSonarQubeEnv('my-sonarqube-server') {
                    sh "${env.scannerHome}/bin/sonar-scanner"
                }            
            } 
        } 
    } 
}
               

