   pipeline { 
    agent any  
    environment { 
        PATH = "/opt/maven/bin:$PATH" 
    } 
    stages { 
        stage('Building') { 
            steps {   
               
                sh 'mvn clean deploy -Dmaven.test.skip=true'   
            
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
                    sh "${scannerHome}/bin/sonar-scanner" 
 
                }            
            } 
        } 
          stage('qualty gate') { 
   steps{ 
     script{ 
	    timeout(time: 1,unt: HOURS) { 
		  def qg= waitForQualityGate() 
		  if (qg.status != OK ) { 
		    
			    echo "Warning: Quality gate failed but continuing pipeline: ${qg.status}"  
		    } 
         } 
       } 
     } 
   }       
 } 
}
               

