node {
	def app
	stage ('Clone repository') {
		checkout scm
	}

	stage('Build image') {
		docker.withDockerServer('docker') {
			app = docker.build 'hello-gitops:latest'
		}
	}

	stage('Test image') {
		app.inside {
			sh 'echo "Tests passed"'
		}
	}

	stage('Push image') {
		docker.withRegistry('https://harbor.defenders.dev/library', 'harbor-defenders') {
			app.push("${env.BUILD_NUMBER}")
		}
	}

	stage('Trigger ManifestUpdate') {
		echo "triggering updatemanifest job"
		build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
	}
}
