pipeline {
  agent any
  stages {
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
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'dockerhub', url:'') {
          sh 'docker push bedrettinyuce/result'
        }
      }
    }
    stage('Push vote image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'dockerhub', url:'') {
          sh 'docker push bedrettinyuce/vote'
        }
      }
    }
    stage('Push worker image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'dockerhub', url:'') {
          sh 'docker push bedrettinyuce/worker'
        }
      }
    }
  }
}