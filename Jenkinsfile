pipeline {
    parameters{
	choice(name: 'deploy')
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
