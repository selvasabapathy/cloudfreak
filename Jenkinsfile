pipeline {
  agent any
    tools {
      maven 'MAVEN384'
      jdk 'JDK8'
    }
    stages {      
        stage('Build maven ') {
            steps { 
                    sh 'pwd'      
                    sh 'mvn  clean install package'
            }
        }
        
        stage('Copy Artifact') {
           steps { 
                   sh 'pwd'
		   sh 'cp -r target/*.jar docker'
           }
        }
         
        stage('Build docker image') {
           steps {
               script {        
                 def customImage = docker.build('selvasabapathy/k8spetclinic', "./docker")
                 docker.withRegistry('https://registry.hub.docker.com', 'SelvaDocker') {
                 customImage.push("${env.BUILD_NUMBER}")
                 }                     
           }
        }
	  }
    }
}
