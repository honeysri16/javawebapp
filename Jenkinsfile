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
         s3Upload consoleLogLevel: 'INFO', dontSetBuildResultOnFailure: false, dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'jenkin-dev2', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'us-east-1', showDirectlyInBrowser: false, sourceFile: '**/*.war', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 's3', userMetadata: []
	    }
}
}
}
