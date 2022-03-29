pipeline {
    agent any
    tools {
    maven 'Maven3.8.4'	
	}
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/honeysri16/javawebapp.git']]])
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install -f pom.xml'
            }
        }
        stage('Deploy to Tomcat') {
            steps {
		    deploy adapters: [tomcat9(credentialsId: 'tomocat-deployer', path: '', url: 'https://github.com/honeysri16/javawebapp.git')], contextPath: /var/lib/jenkins/workspace/multi-pipeline_master@2, war: '**/*.war'
            }
        }
    }
}
