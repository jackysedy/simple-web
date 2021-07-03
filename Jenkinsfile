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
        	    sh '''#!/bin/bash
			set -x
			az login --identity
			az aks get-credentials --admin --name jacky-interview-aks --resource-group devops-interview-rg
			kubectl get pods -n default | grep simple-web
			exists=$(echo $?)
			kubectl get pods -n default | grep simple-web | grep Terminating
			Terminating=$(echo $?)
			if [ "$selection" == "deploy" ];then
			    if [ "$exists" = 1 ] || [ "$Terminating" == 0 ]; then
				echo "deploying simple-web"
				helm install simple-web .
			    fi
			fi
                       	
			if [ "$selection" == "destroy" ];then
			    if [ "$exists" = 0 ] && [ "$Terminating" == 1 ] ; then
				echo "destroying simple-web"
				helm uninstall simple-web 	    
			    fi
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
