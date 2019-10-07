node {
    def newApp
    def registry = 'https://registry-1.docker.io/v2/'
		def imagename = "frenzy669/bamba-pro"
    def registryCredential = 'dockerhub'
		def branch = env.BRANCH_NAME
		def buildName
		def tag = "$branch"+"_"+"$BUILD_NUMBER"
	
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
		  buildName = imagename + ":$tag"
			newApp = docker.build(buildName)
			newApp.push()
      newApp.push('latest')
  	}
		stage('Deploy') {
		sh "sudo helm upgrade todo1 todo/. --recreate-pods --set image.tag=$tag"
	}
	}
}