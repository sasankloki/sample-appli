pipeline{

	agent {label 'linux'}

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/sasankloki/sample-appli/tree/master/tempdir.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t sasankloki/webapp:1 .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push sasankloki/webapp:1'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}