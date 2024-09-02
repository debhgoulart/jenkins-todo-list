pipeline {         
	agent none         
	stages {                  	

		stage ("build & SonarQube Analysis") {                         
			agent any                         
			steps {                                 
				withSonarQubeEnv("jenkins-todolist") {                                         
					sh 'mvn clean package sonar:sonar'                                 
				}                         
			}                 	
		}         	
	} 
}
