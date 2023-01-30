node {
    checkout scm

    docker.withServer('tcp://10.233.102.187:2376, 'dind') {
	def app = docker.build('hello docker')
    }
}
