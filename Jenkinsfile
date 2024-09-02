pipeline {         
	agent none         
	stages {                  	

		stage ("build & SonarQube Analysis") {                         
			agent any                         
			steps {                                 
				stage('build & SonarQube Analysis') {
					steps {                                         
						sh 'npm install'
						sh 'npm run build'
						sh 'sonar-scanner'
					}                                 
				}                         
			}                 	
		}         	
	} 
}
