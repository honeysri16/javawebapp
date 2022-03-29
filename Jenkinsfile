pipeline {
	parameters {
		choice(choices: ['Dev', 'QA'], description: 'Target for build  env', name: 'env')
		choice(choices: ['Y','N'], description: 'is the deployment for release' , name: 'isRelease')
	}
	
    agent any
    tools {
    maven 'Maven3.8.4'	
	}
    stages {
        stage('Checkout') {
            steps { 
		    checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/honeysri16/javawebapp.git']]]
			  }
			     }
   }
        stage('Build') {
            steps {
                sh 'mvn clean install -f pom.xml'
            }
        }
        //stage('Deploy to Tomcat') {
          //steps {
                //deploy adapters: [tomcat9(credentialsId: 'tomcat-deployer', path: '', url: 'http://52.45.81.16//')], contextPath: null, war: '**/*.war'
	 // }
	//}
    }
}
