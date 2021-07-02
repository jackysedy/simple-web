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
		    sh 'printenv'
		    sh 'helm'	
		    sh 'ls'	
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
