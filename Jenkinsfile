pipeline {
	agent any
	enviroment {
		//variaveis de ambiente
		VIRTUALENV_NAME = 'venv-django-todolist'
		scanner_home = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
	}
	stages {
		stage('Checkout') {
			steps {
				checkout scm
			}
		}
		stage('Setup Virtualenv and Install Dependencies') {
			steps {
				sh '''
					sudo pip3 install virtualenv
					virtualenv --always-copy ${VIRTUALENV_NAME}
					source ${VIRTUALENV_NAME}/bin/activate
					pip install -r requirements.txt
				'''
			}
		}
		stage('Run Migrations') {
			steps {
				sh '''
					source ${VIRTUALENV_NAME}/bin/activate
					python manage.py makemigrations
					python manage.py migrate
				'''
			}
		}
		stage('SonarQube Analysis') {
			steps {
				withSonarQubeEnv('sonar-server') {
					sh '''
						source ${VIRTUALENV_NAME}/bin/activate
						${SCANNER_HOME}/bin/sonar-scanner \
						-Dsonar.projectKey=jenkins-todolist \
						-Dsonar.sources=. \
						-Dsonar.python.version=2.7.17 \
						-Dsonar.sourceEncoding=UTF-8
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
