node {
    def newApp
    def registry = 'https://registry-1.docker.io/v2/'
		def imagename = "frenzy669/bamba-pro"
    def registryCredential = 'dockerhub'
		def branch = env.BRANCH_NAME
	
	stage('Git') {
		git 'https://github.com/daniel-git574/todoapp.git'
	}
	stage('Build') {
		sh 'npm install'
	}
	stage('Test') {
		sh 'npm test'
	}
	stage('Building image') {
      docker.withRegistry( registry, registryCredential ) {
		  def buildName = imagename + ":$branch_$BUILD_NUMBER"
			newApp = docker.build(buildName)
			newApp.push()
      newApp.push('latest')
  	}
	}
}