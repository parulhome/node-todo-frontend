node {
    env.AWS_ECR_LOGIN=true
    def newApp
    def registry = 'singhparul/mydevopstest'
    def registryCredential = 'dockerhub'
    def dockerImage = ''
	
	stage('Git') {
		git 'https://github.com/parulhome/node-todo-frontend'
	}
	stage('Build') {
		sh 'npm install'
	}
	stage('Test') {
		sh 'npm test'
	}
	/*
	stage('Building image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
		    def buildName = registry + ":$BUILD_NUMBER"
			newApp = docker.build buildName
			newApp.push()
        }
	}*/
	
	stage('Building our image') { 
            steps { 
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            } 
        }

	stage('Registring image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
    		newApp.push 'latest2'
        }
	}
    stage('Removing image') {
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker rmi $registry:latest"
    }
    
}
