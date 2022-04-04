pipeline {
	agent any
	stages {
	  stage('Lint python script') {
		  steps {
			  sh 'pylint *.py'
		  }
	  }
		stage('Build Docker Image') {
			steps {
				withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]){
					sh '''
						docker build -t sasankloki/webapp:1 .
					'''
				}
			}
    }

		stage('Push Image To Dockerhub') {
			steps {
				withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]){
					sh '''
						docker login -u sasankloki -p LOKI@sasank96
						docker push sasankloki/webapp:1
					'''
				}
			}
		}

	
	

	}
}