pipeline {
    agent any
	

	
    stages {
      
        stage('MVN CLEAN') {
            steps {
               
              script {

                  sh 'mvn clean'

 
                      }
                   }        
         }
        stage('MVN compile') {
            steps {
               
              script {

                  sh 'mvn compile'

 
                      }
                   }        
         }
         stage('MVN INSTALL') {
            steps {
               
              script {

                  sh 'mvn install'

 
                      }
                   }        
         }
	 stage('SONAR') {
            steps {
               
              script {
		
                   
                  sh 'mvn sonar:sonar  -Dsonar.sources=src/main/java -Dsonar.css.node=. -Dsonar.java.binaries=. -Dsonar.host.url=http://192.168.0.101:9000/ -Dsonar.login=admin   -Dsonar.password=sonar'

 
                      }
                   }         
         }
	    
	     stage('MVN package') {
            steps {
                script {
                    
                sh 'mvn package'  
                }

		        
            } 
           
        }
         
        stage('nexus') {
            steps {
               
              script {

sh 'mvn deploy -e'                      }
                   }         
         }
	 stage('Building our image') {
  steps {
               
sh 'docker build -t oussamahasni/examthouraya .'
               
            }
        }
	    
	stage('docker login') {
            steps {
                script {
                   
                        sh 'docker login --username oussamahasni --password 203JMT0329' 
                    }
                    
                }
                
            
            
        } 
stage('Push Dockerhub') {
            steps {
                script {
                   
                        sh "docker push oussamahasni/examthouraya "
                    }
                    
	    }   
        }
	    stage('Run Spring et MySQL Containers') {
                                steps {
                                    script {
                                      sh ' docker-compose up -d '
                                    }
                                }
                            }    
	    
	    
	    
	    
	    
     }
	post {
         always {
            junit(testResults: 'target/surefire-reports/*.xml', allowEmptyResults : true)
        }
         success {
            emailext attachLog: true, body: '''End of Pipeline
            Finished: SUCCESS''', subject: '#Success', to: 'oussama.hasni1@esprit.tn'
         }
         failure  {
            emailext attachLog: true, body: '''End of Pipeline
            Finished: FAILURE''', subject: '#Failure', to: 'oussama.hasni1@esprit.tn'
         }
     
    }
     
}
