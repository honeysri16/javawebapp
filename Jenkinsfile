pipeline {
	parameters {
		choice(choices: ['Dev', 'QA'], description: 'Target for build  env', name: 'env')
		choice(choices: ['Y','N'], description: 'is the deployment for release' , name: 'isRelease')
	}
	
    agent any
    tools {
    maven 'Maven3.8.4'
    }
	options {
        withAWS(profile:'default')
        }
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/keyspaceits/javawebapp.git']]])
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install -f pom.xml'
            }
	}
	stage('S3Bucket') {
                 steps {
       s3Upload(acl: 'Private', bucket:"jenkins-dev2", cacheControl: '', excludePathPattern: '', file: 'CounterWebApp.war', workingDir:'/var/lib/jenkins/workspace/multi-pipeline_master/target/')
}
    }
}
}
