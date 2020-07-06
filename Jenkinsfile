pipeline {
  agent any
  stages {
    stage('Snyk scan') {
	  steps {
		snykSecurity additionalArguments: '--all-projects', snykInstallation: 'snyk', snykTokenId: 'SNYK_TOKEN'
	  }
	}
    stage('Build result') {
      steps {
        sh 'docker build -t bedrettinyuce/result ./result'
      }
    } 
    stage('Build vote') {
      steps {
        sh 'docker build -t bedrettinyuce/vote ./vote'
      }
    }
    stage('Build worker') {
      steps {
        sh 'docker build -t bedrettinyuce/worker ./worker'
      }
    }
    stage('Push result image') {
      steps {
        withDockerRegistry(credentialsId: 'dockerhub', url:'') {
          sh 'docker push bedrettinyuce/result'
        }
      }
    }
    stage('Push vote image') {
      steps {
        withDockerRegistry(credentialsId: 'dockerhub', url:'') {
          sh 'docker push bedrettinyuce/vote'
        }
      }
    }
    stage('Push worker image') {
      steps {
        withDockerRegistry(credentialsId: 'dockerhub', url:'') {
          sh 'docker push bedrettinyuce/worker'
        }
      }
    }
	stage('Deploy to Kubernetes') {
	  steps {
	    kubernetesDeploy configs: 'kube-deployment.yml', kubeConfig: [path: ''], kubeconfigId: 'kubeconf', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
      }
	}
  }
}