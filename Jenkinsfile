pipeline {
    agent any
    stages {

	stage('Clone repository'){
		checkout scm
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
