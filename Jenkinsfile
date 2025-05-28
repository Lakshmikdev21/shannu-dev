pipeline {
    agent any
 
    stages {
        stage('Clone') {
            steps {
                git credentialsId: 'github', url: 'https://github.com/Lakshmikdev21/shannu-dev.git'
            }
        }
          stage('Build') {
            steps {
               bat 'mvn clean install'
            }
        }
	    stage('Test') {
            steps {
               bat 'mvn test'
            }
        }
          stage('Generate Artifacts') {
            steps {
               archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
            }
        }
		stage('Deploy to Tomcat Server') {
        steps {
            deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'Tomcat', path: '', url: 'http://localhost:8080')], contextPath: 'SHANNU CALCY', war: 'target/*.war'
        }
    }
    }
}
