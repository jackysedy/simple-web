pipeline {
    parameters{
	choice(
	    choices: ['deploy','destroy'],	
	    name: 'selection'
        )		
    }	    
    agent any
    options {
        timestamps()
        timeout(time: 2, unit: 'HOURS')
	    buildDiscarder logRotator(daysToKeepStr: '20', numToKeepStr: '50')
    }
    stages{
        stage('Describe') {
	        steps {
		        script {	
        		    sh '''
        		        az login --identity
        		        az aks get-credentials --admin --name jacky-interview-aks --resource-group devops-interview-rg
        		        if [ "$selection" == "deploy" ]; then
                            		echo "deploying simple-web"
                            		helm install simple-web .
                       		 else
                            		echo "destroying simple-web"
                           		 helm uninstall simple-web 
                       		 fi
        		        
        		    '''	
		        }
	        }
	  }
    }	
    post {
	    always {
	        cleanWs()
	    }
   }
}
