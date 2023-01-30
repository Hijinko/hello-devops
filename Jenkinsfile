node {
    checkout scm

    docker.withServer('docker', 'dind') {
	def app = docker.build('hello-gitops')
    }
}
