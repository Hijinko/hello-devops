node {
	def app
	stage ('Clone repository') {
		checkout scm
	}

	stage('Build image') {
		app = docker.build("raj80dockerid/test")
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
