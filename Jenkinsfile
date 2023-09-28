pipeline {

	agent {
	  label 'Jenkins1'
	}
	
 tools {
	maven "maven.3.9.4"
 }
 
 stages {
	stage('1.CloneCode') {
		steps {
			sh "echo cloning latest code release"
		git url: 'https://github.com/Teemania30/maven-web-application.git'
			sh "echo cloning successful"
		}
	}
	stage('2.CodeQualityAnalysis'){
		steps {
			sh "echo Running Code Quality Analysis"
			sh "mvn sonar:sonar"
		}
	
	}
	stage ('3.BuildArtifact'){
		steps {
		sh "echo validating, compiling, testing and package"
		sh "mvn clean package"
		sh "echo validating, compiling, testing and package successful"
		}
	}
	stage ('4.DeployArtifact'){
		steps {
			sh "echo PushingArtifact2Nexus"
			sh "mvn deploy"
		}
	}
	stage ('5.Deploy2Tomcat'){
		steps {
			deploy adapters: [tomcat9(credentialsId: 'Tomcat-Credentials', path: '', url: 'http://16.170.158.135:8080/')], contextPath: null, war: 'target/*.war'
		}
	}
 }
}
