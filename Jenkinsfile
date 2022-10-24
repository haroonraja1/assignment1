pipeline {
    agent any
    environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-cred')
	}
    stages {
        stage('Build') {
            steps {
                sh 'sudo docker container prune -f'
                sh 'sudo docker build . -t iamharoon/c27001'
            }
        }

        stage('Run') {
            steps {
                sh 'sudo service docker stop'
                sh 'sudo service docker start'
                sh 'sudo docker run -d -p 81:8081 -d iamharoon/c27001'
            }
        }

        stage('Push to Dockerhub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'sudo docker push iamharoon/c27001'
            }
        }
    }
    post {
		always {
			sh 'sudo docker logout'
		}
	}
}
