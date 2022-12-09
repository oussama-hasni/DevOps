pipeline {
    agent any
	


    stages {
        stage('Getting the project from GIT') {
            steps {
               echo 'Test';
            }
        }
        
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
