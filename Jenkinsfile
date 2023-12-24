pipeline {
    agent any

	tools {
    jdk 'Java 1.8'

  }

    stages {
        stage('CLONE SCM') {
            steps {
                echo 'cloning code from Github'
				git branch: 'main', url: 'https://github.com/rsandeep47/App2.git'
            }
        }
			
		stage('SONARQUBE ANALYSIS') {
            steps {
                echo 'SONARQUBE ANALYSIS'
				sh 'mvn clean sonar:sonar'
            }
        }
		
		
		stage('Build Artifact AND PUSHING TO NEXUS') {
            steps {
                echo 'Build Artifact with maven build tool'
				sh 'mvn clean deploy'
            }
        }
		
		stage('Deploy') {
            steps {
                echo 'Deploy to tomcat ap/n server '
				deploy adapters: [tomcat9(credentialsId: 'Tomcatcred', path: '', url: 'http://52.91.153.52:8081/')], contextPath: 'app2', war: '**/*.war'
            }
        }
    }
}
