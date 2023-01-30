pipeline {
    agent any
    stages {

	stage('Clone repository'){
		steps {
		 git 'https://github.com/Hijinko/hello-devops.git'
		}
	}

        stage('Build Docker Image') {
            steps {
                docker.withDockerServer('mydockerhost') {
                    sh 'docker build -t myimage .'
                }
            }
        }
    }
}
