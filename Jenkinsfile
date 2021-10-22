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
	
	stage('Building our image') { 
    
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }

	stage('Deploy our image') { 
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push() 
            }
        }
	/*
       stage('Cleaning up') { 
                sh "docker rmi $registry:$BUILD_NUMBER" 

        } */
	
	stage('Deploy to k8s') { 
		
	  kubernetesDeploy(
   		 kubeconfigId: 'kubeconfig',
   		 configs: 'deploy.yml',
   		 enableConfigSubstitution: true
	 )	

        }
	
    
}
